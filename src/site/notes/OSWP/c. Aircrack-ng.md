---
{"dg-publish":true,"permalink":"/OSWP/c. Aircrack-ng/"}
---

-------------------------
### Airmon-ng
	Enable and disable monitor mode on various interfaces
- Display status and info about wireless interfaces (append --verbose/debug for more):
```
sudo airmon-ng
```
- Identify processes which may interfere with the tools:
```
sudo airmon-ng check
```
- Kill the processes gently:
```
sudo airmon-ng check kill
```
- Place wlan0 in monitor mode (append channel number if neccessary):
```
sudo airmon-ng start wlan0
```
- List info about monitor interface:
```
sudo iw dev wlan0mon info
```
- Disable monitor mode:
```
sudo airmon-ng stop wlan0mon
```

--------
### Airodump-ng
	Capture raw 802.11 frames and export in various formats
- Display filter and capture options:
```
sudo airodump-ng
```
- Sniff on specified channel:
```
sudo airodump-ng wlan0mon -c 2
```
- Top section capture fields description:
![Pasted image 20231108154624.png](/img/user/IMAGES/Pasted%20image%2020231108154624.png)
- Bottom section capture fields descriptions:
![Pasted image 20231108154831.png](/img/user/IMAGES/Pasted%20image%2020231108154831.png)
- Sniff specified BSSID and channel + write to file:
```
sudo airodump-ng -c 3 --bssid 34:08:04:09:3D:38 -w cap1 wlan0mon
```
- Interactive mode keys:
 ![Pasted image 20231108155538.png|525](/img/user/IMAGES/Pasted%20image%2020231108155538.png)
- If SSIDs are displayed as lengths the AP is too far away.

------
### Aireplay-ng
	Used for generating wireless traffic
- Supports the following attacks:
  ![Pasted image 20231108160044.png](/img/user/IMAGES/Pasted%20image%2020231108160044.png)
- Available options:
  ![Pasted image 20231108160137.png](/img/user/IMAGES/Pasted%20image%2020231108160137.png)
- General injection test:
```
sudo aireplay-ng -9 wlan0mon
```
- Specific injection test:
```
sudo aireplay-ng -9 -e wifu -a 34:08:04:09:3D:38 wlan0mon
```
- Card-to-Card injection test:
```
sudo aireplay-ng -9 -i wlan1mon wlan0mon
```

----------
### Aircrack-ng
	Offline packet capture AP cracking tool
- Benchmark test:
```
aircrack-ng -S  
```


----
### Airdecap-ng
	Packet capture decrypt tool
- Filter out APs from capture file:
```
sudo airdecap-ng -b 34:08:04:09:3D:38 opennet-01.cap
```


------
### Airgraph-ng
	Python script to create graphs of wireless networks
- Clients to AP Relationship (CAPR) graph
	- Won't draw AP that doesn't have any clients
	- Assigns colours to APs depending on encryption
		- WPA: green
		- WEP: yellow
		- Open: red
		- Black: unknown
	- Usage:
```
airgraph-ng -o Picture1_png -i dump-01.csv -g CAPR
```
- Client Probe Graph (CPG)
	- Displays relationship between wireless clients and probed networks
	- Usage:
```
airgraph-ng -o Picture2.png -i dump-01.csv -g CPG
```