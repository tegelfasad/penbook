---
{"dg-publish":true,"permalink":"/oswp/k-chipset-and-drivers/","updated":"2024-01-05T11:37:26.725+01:00"}
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