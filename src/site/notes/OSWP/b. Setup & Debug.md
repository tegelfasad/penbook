---
{"dg-publish":true,"permalink":"/oswp/b-setup-and-debug/"}
---


------------------
### Determine wireless device driver:
```
sudo airmon-ng --verbose
```
### Determine USB devices:
```
sudo lsusb -vv
```
### List info about driver:
```
sudo modinfo <driver-name>
```
### List all loaded modules:
```
lsmod
```
### Change parameter in driver:
```
sudo modprobe <driver-name> <setting>=<value>
```
### Remove driver-dependent module before unloading it:
```
sudo rmmod <driver-name> <dependency>
```
### List interface detectable frequencies with iwconfig:
```
sudo iwlist wlan0 frequency
```
### List wireless interface details:
```
sudo iw list
```
### Scan for available SSIDs:
```
sudo iw dev wlan0 scan | egrep "DS Parameter set|SSID:"
```
### Add and activate new monitor interface:
```
sudo iw dev wlan0 interface add wlan0mon type monitor
sudo ip link set wlan0mon up
```
### Sniff traffic from monitor interface:
```
sudo tcpdump -i wlan0mon
```
### Delete monitor interface:
```
sudo iw dev wlan0mon interface del
```
### Fetch radio regulatory domain:
```
sudo iw reg get
```
### Temporarily change reg domain:
```
sudo iw reg set <country-id>
```
### Display enabled radio devices:
```
sudo rfkill list
```
### Block/unblock radio device:
```
sudo rfkill block/unblock <device-number>/all
```
### Set wlan0 to monitor mode:
```
sudo ip link set wlan0 down
sudo iwconfig wlan0 mode monitor
sudo ip link set wlan0 up
```
### Scan all 2.4GHz channels with channel hop:
```
#!/bin/bash
for channel in 1 6 11 2 7 10 3 8 4 9 5
do
  iw dev wlan0mon set channel ${channel}
  sleep 1
done
```
### Scan using airodump:
```
sudo airodump-ng wlan0mon
```
### Start wireshark with parameters from CLI:
```
sudo wireshark -i wlan0mon -k -f "not subtype beacon"
```
### TCPdump to STDOUT:
```
sudo tcpdump -i wlan0mon -w - -U
```
### DumpCap to STDOUT:
```
sudo dumpcap -w - -P -i wlan0mon
```
### Unnamed pipe STDOUT Wireshark capture:
```
sudo tshark -w - -i wlan0mon
```
### Named pipe STDOUT capture:
```
mkfifo /tmp/<pipe-name>
sudo wireshark -k -i /tmp/<pipe-name>
sudo tcpdump -U -w - -i wlan0mon > /tmp/<pipe-name>
```
### Remote packet capture to local Wireshark:
```
ssh root@10.11.0.196 "sudo -S tcpdump -U -w - -i wlan0mon" | sudo wireshark -k -i -
```
### Generate WPA Enterprise PSK:
```
wpa_passphrase <ssid>
```
