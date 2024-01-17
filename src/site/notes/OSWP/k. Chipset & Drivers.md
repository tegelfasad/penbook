---
{"dg-publish":true,"permalink":"/OSWP/k. Chipset & Drivers/"}
---

---------------
### Determining the Wireless Chipset:

#### Physical access:
FCC ID into https://fcc.gov/

#### Remote access:
```
#Check using airmon:
airmon-ng

#Check from loaded modules before/after:
lsmod

#Check kernel info before/after:
dmesg

#Check USB connections:
sudo lsusb -vv
lspci -n
```