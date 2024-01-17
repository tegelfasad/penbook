---
{"dg-publish":true,"permalink":"/OSWP/a. Wireless Theory/"}
---

-------------------
- Mesh: all APs are equal without defined roles, extends network reach
- Wireless Distribution Systems (WDS): multiple APs connected with a distributed system such as main AP
- Wireless Bridging: allows WDS APs to communicate
- Wireless Repeating: allows both stations and APs to communicate
- Wi-Fi Direct/P2P: devices allows for direct communication without passing the AP first by acting as a software AP using WPS-style connection, eg. internet sharing and file sharing

### Network connection steps:
1. The client sends an authentication request to the AP
2. The AP sends an authentication response of "successful"
3. The client sends an association request to the access point
4. The AP sends an association response if the capability of the clients meets that of the AP

![Pasted image 20231101150330.png|475](/img/user/IMAGES/Pasted%20image%2020231101150330.png)

### Wire Equivalent Privacy (WEP)
1. CRC is appended to plaintext message
2. Message is XORed with key stream which is derived from a concatenation of the secret key and the initialization vector (the seed). The seed is 64 or 128 bits
3. Encrypted message is sent together with IV to be checked at the receiver from the secret key that is shared
- RC4 encryption
	- Symmetric cipher
	- Key stream is XOR'd with plain text
	- Two elements:
		- Key Scheduling Algorithm (KSA): Initializes state table with IV and WEP key
		- Pseudo-Random Generation Algorithm (PRGA): Creates the keystream
		- ![Pasted image 20231101150752.png|525](/img/user/IMAGES/Pasted%20image%2020231101150752.png)
- C32 checksums using ICV

### WEP Authentication
- Open authentication: client does not provide any credentials, hence everyone can connect
- Shared authentication: challenge text is sent to client, must be encrypted with WEP key and sent for verification

### WPA Ciphers:
- TKIP/WPA1: legacy hardware that can only handle WEP
- CCMP/RSN/WPA2: based on AES

### Tools, drivers, and stacks
- In Linux one driver can cover multiple devices of same chipset
- Most drivers are Loadable Kernel Modules (LKM) which are only loaded when necessary
- Drivers are located in:
```
/lib/modules/<kernel-version>
```
- Vermagic indicates for what system the driver was compiled
- Firmware states what can be loaded by driver
- Some modules may need to be blacklisted if multiple drivers fight for the same resources

### Wireless tools
- Two sets of tools: iw (new), and iwconfig (legacy)
- _iwconfig_ manipulates the basic wireless parameters: change modes, set channels, and keys.
- _iwlist_ allows for the initiation of scanning, listing frequencies, bit rates, and encryption keys.
- _iwspy_ provides per-node link quality (not often implemented by drivers).
- _iwpriv_ allows for the manipulation of the Wireless Extensions specific to a driver.

### Wireshark setup:
- _Edit_ > _Preferences_ > _Appearance_ > _Layout_ > Layout 2
- _View_ > _Wireless Toolbar_
- Coloring rule filters: https://wiki.wireshark.org/ColoringRules

### Wireshark capture filters
- "not subtype beacon" : ignores AP beacon frames
- MAC adress + beacon filter:
```
((wlan addr1 3A:30:F9:0F:E1:95) or (wlan addr2 3A:30:F9:0F:E1:95) or (wlan addr3 3A:30:F9:0F:E1:95) or (wlan addr4 3A:30:F9:0F:E1:95)) and (not subtype beacon)
```

### Remote Wireshark capture with SSHdump:
1. Choose "External Capture" and configure SSH settings
2. To use standard user:
```
sudo dpkg-reconfigure wireshark-common / yes
sudo usermod -a -G wireshark kali
```

