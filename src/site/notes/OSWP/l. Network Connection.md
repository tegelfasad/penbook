---
{"dg-publish":true,"permalink":"/oswp/l-network-connection/"}
---

-------
### Connect interface using wpa_supplicant:
1. Create .conf:
```
network={
  ssid="home_network"
  scan_ssid=1
  psk="password123"
  key_mgmt=WPA-PSK
}
```
2. Connect:
```
sudo wpa_supplicant -i wlan0 -c wifi-client.conf -B
```
3. Request DHCP-lease:
```
sudo dhclient wlan0
```

---------
### Setting up an AP
1. Check what modes all interfaces support:
```
sudo iw list
```
2. Enable interface:
```
sudo ip link set wlan0 up
```
3. Configure IP range that does not conflict regular network:
```
sudo ip addr add 10.0.0.1/24 dev wlan0
```
4. Configure DNS and DHCP server config:
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
listen-address=10.0.0.1

# DHCP range
dhcp-range=10.0.0.100,10.0.0.199,12h
dhcp-lease-max=100
# Router: wlan0
dhcp-option=option:router,10.0.0.1
dhcp-authoritative

# DNS: Primary and secondary Google DNS
server=8.8.8.8
server=8.8.4.4
```
5. Run dnsmasq with the configuration file:
```
sudo dnsmasq --conf-file=dnsmasq.conf
```
6. Confirm the server is running:
```
sudo tail /var/log/syslog | grep dnsmasq
```
7. Set up forwarding rules:
```
#Enable IP forwarding:
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward

#Add NAT table:
sudo nft add table nat

#Add chain for postrouting:
sudo nft 'add chain nat postrouting { type nat hook postrouting priority 100 ; }'

#Add masquerading rule:
sudo nft add rule ip nat postrouting oifname "eth0" ip daddr != 10.0.0.1/24 masquerade
```
8. Create AP configuration file:
```
interface=wlan0
ssid=<network-name>
channel=11

# 802.11n
hw_mode=g
ieee80211n=1

# WPA2 PSK with CCMP
wpa=2
wpa_key_mgmt=WPA-PSK
rsn_pairwise=CCMP
wpa_passphrase=<passkey>
```
9. Run conf file with hostapd:
```
sudo hostapd file.conf
```
-B for background