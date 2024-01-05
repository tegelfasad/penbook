---
{"dg-publish":true,"permalink":"/oswp-playbook/"}
---

-------------
## 1. Wireless Configuration

#### 1.1. Drivers & Modules
- [[2. OSWP/2. Setup & Debug#Determine wireless device driver\|List devices & drivers]]
- [[2. OSWP/2. Setup & Debug#List info about driver\|More driver info]]
- [[2. OSWP/2. Setup & Debug#List all loaded modules\|List loaded modules]]
- [[2. OSWP/2. Setup & Debug#Change parameter in driver\|Edit modules]]
- [[2. OSWP/2. Setup & Debug#Remove driver-dependent module before unloading it\|Remove modules]]
- [[2. OSWP/2. Setup & Debug#Determine USB devices\|List USB devices]]
#### 1.2. Wireless Interfaces
- [[2. OSWP/2. Setup & Debug#List wireless interface details\|List wireless interfaces]]
- [[2. OSWP/2. Setup & Debug#List interface detectable frequencies with iwconfig\|List interface detectable frequencies]]
- [[2. OSWP/2. Setup & Debug#Add and activate new monitor interface\|New monitor interface]]
- [[2. OSWP/2. Setup & Debug#Delete monitor interface\|Delete monitor interface]]
#### 1.3. Wireless Chipsets
- Determining Chipset:
	- [[2. OSWP/11. Chipset & Drivers#Physical access\|Physical access]]
	- [[2. OSWP/11. Chipset & Drivers#Remote access\|Remote access]]
#### 1.4. Radio Devices
- [[2. OSWP/2. Setup & Debug#Fetch radio regulatory domain\|Fetch regulatory radio domain]]
- [[2. OSWP/2. Setup & Debug#Temporarily change reg domain\|Change domain]]
- [[2. OSWP/2. Setup & Debug#Display enabled radio devices\|List enabled radio devices]]
- [[2. OSWP/2. Setup & Debug#Block/unblock radio device\|Block/unblock radio device]]
--------------------
## 2. Scanning & Capture

#### 2.1. Scanning
- [[2. OSWP/2. Setup & Debug#Set wlan0 to monitor mode\|Enable monitor mode]]
- [[2. OSWP/2. Setup & Debug#Scan for available SSIDs\|Scan available networks]]
- [[2. OSWP/2. Setup & Debug#Scan all 2.4GHz channels with channel hop\|Manual channel scanning]]
- [[2. OSWP/2. Setup & Debug#Scan using airodump\|Airodump scan]]
#### 2.2. Wireshark
- [[2. OSWP/1. Wireless Theory#Wireshark setup\|Wireshark setup]]
- [[2. OSWP/1. Wireless Theory#Wireshark capture filters\|Authentication analysis filter]]
- [[2. OSWP/2. Setup & Debug#Start wireshark with parameters from CLI\|Start Wireshark from params]]
- [[2. OSWP/1. Wireless Theory#Remote Wireshark capture with SSHdump\|Remote capture with SSHdump]]
- [[2. OSWP/2. Setup & Debug#Remote packet capture to local Wireshark\|Remote capture from SSH session]]
#### 2.3. CLI Packet Capture
- [[2. OSWP/2. Setup & Debug#TCPdump to STDOUT\|TCPdump]]
- [[2. OSWP/2. Setup & Debug#DumpCap to STDOUT\|DumpCap]]
- [[2. OSWP/2. Setup & Debug#Unnamed pipe STDOUT Wireshark capture\|Tshark]]
- [[2. OSWP/2. Setup & Debug#Named pipe STDOUT capture\|Wireshark using named pipe]]
----
## 3. Aircrack Suite

- [[2. OSWP/3. Aircrack-ng#Airmon-ng\|Airmon (Monitor mode)]]
- [[2. OSWP/3. Aircrack-ng#Airodump-ng\|Airodump (Packet capture)]]
- [[2. OSWP/3. Aircrack-ng#Aireplay-ng\|Aireplay (Spoofing traffic)]]
- [[2. OSWP/3. Aircrack-ng#Aircrack-ng\|Aircrack (Packet cracking)]]
- [[2. OSWP/3. Aircrack-ng#Airdecap-ng\|Airdecap (Packet decrypt)]]
- [[2. OSWP/3. Aircrack-ng#Airgraph-ng\|Airgraph (Network graphs)]]
- [[2. OSWP/4. PSK Cracking#Airolib-ng\|Airolib (Rainbow tables)]]
--------
## 4. Wireless Attacks

#### 4.1. PSK Cracking
- [[2. OSWP/4. PSK Cracking#Crack walkthrough\|Attack walkthrough]]
- Offline Packet Cracking:
	- [[2. OSWP/4. PSK Cracking#John cracking\|John]]
	- [[2. OSWP/4. PSK Cracking#Hashcat\|Hashcat]]
- Mutating Wordlists:
	- [[2. OSWP/4. PSK Cracking#Crunch\|Crunch]]
	- [[2. OSWP/4. PSK Cracking#RSMangler\|RSMangler]]
- Rainbow Tables:
	- [[2. OSWP/4. PSK Cracking#Airolib-ng\|Airolib PMKs]]
	- [[2. OSWP/4. PSK Cracking#coWPAtty\|coWPAtty]]
#### 4.2. WPS Attacks
- [[2. OSWP/5. WPS Cracking#Scan for APs with WPS\|Scan for WPS]]
- Attacks:
	- [[2. OSWP/5. WPS Cracking#Reaver default attack\|Default attack]]
	- [[2. OSWP/5. WPS Cracking#PixieWPS attack\|PixieWPS attack]]
	- [[2. OSWP/5. WPS Cracking#BSSID-dependent PIN attack\|BSSID attack]]
- [[2. OSWP/5. WPS Cracking#Common errors\|Common problems]]
#### 4.3. Rouge AP Evil-twin
- [[2. OSWP/6. Rouge APs#Match AP encryption details\|Attack walkthrough]]
- [[2. OSWP/6. Rouge APs#WPA-3 conf\|WPA-3 configuration]]
#### 4.4. WPA Enterprise Attack
- [[2. OSWP/7. Enterprise Cracking#Walktrough\|Attack walkthrough]]
- [[2. OSWP/7. Enterprise Cracking#Theory\|WPA Enterprise theory]]
- [[2. OSWP/2. Setup & Debug#Generate WPA Enterprise PSK\|Generate PSK]]
#### 4.5. Captive Portal Attacks
- [[2. OSWP/8. Captive Portals#Set up php portal\|1. PHP-site setup]]
- [[2. OSWP/8. Captive Portals#Set up DHCP and DNS\|2. DHCP & DNS]]
- [[2. OSWP/8. Captive Portals#Final configs\|3. Final configs]]
- [[2. OSWP/8. Captive Portals#Weird captive portal behavior\|Common problems]]
-------
## 5. Bettercap & Kismet

#### 5.1. Bettercap
	Swiss Army Knife of Network Hacking
- [[2. OSWP/9. Bettercap#Getting started\|Running Bettercap]]
- [[2. OSWP/9. Bettercap#Discovery\|Scanning & discovery]]
- [[2. OSWP/9. Bettercap#Filtering & sorting\|Filtering & sorting]]
- [[2. OSWP/9. Bettercap#Tickers\|Tickers]]
- [[2. OSWP/9. Bettercap#Deauth & handshakes\|Deauth & handshakes]]
- [[2. OSWP/9. Bettercap#Caplets\|Caplet files]]
- [[2. OSWP/9. Bettercap#Bettercap Web Interface\|Web interface]]
#### 5.2. Kismet ()
	Capture and Store Multiple Wireless Capture Sources
- [[2. OSWP/10. Kismet#Running\|Running Kismet]]
- [[2. OSWP/10. Kismet#Configuration\|Configuration files]]
- [[2. OSWP/10. Kismet#Output\|Output options]]
- [[2. OSWP/10. Kismet#Remote Capture\|Remote capture]]
------------------------------
## 6. Network Connection

#### 6.1. Connecting to AP
- [[2. OSWP/12. Network Connection#Connect interface using wpa_supplicant\|Connect interface using wpa_supplicant]]
#### 6.2. Setting up AP
- [[2. OSWP/12. Network Connection#Setting up an AP\|Set up AP walkthrough]]
-------------
