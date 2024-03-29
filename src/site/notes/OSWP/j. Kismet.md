---
{"dg-publish":true,"permalink":"/oswp/j-kismet/"}
---

-----
	Versatile wireless capture tool that can capture data of multiple different wireless technologies

Installation:
```
sudo apt install kismet
```
-----------
## Configuration
- Config files found in /etc/kismet/
- By creating a new .conf file in the directory other files are overridden
- Different configuration files:
	- kismet_80211.conf configures settings related to Wi-Fi.
	- kismet_alerts.conf configures Kismet's intrusion detection and alert subsystem. Kismet includes a _Wireless Intrusion Detection System_ (WIDS), but we will not cover that particular functionality in this module.
	- kismet.conf is the master configuration file for Kismet.
	- kismet_filter.conf configures filtering rules for devices and packets.
	- kismet_httpd.conf configures Kismet's web server.
	- kismet_logging.conf configures how and where Kismet creates log files
	- kismet_memory.conf configures Kismet's memory usage.
	- kismet_uav.conf contains rules for detecting unmanned aerial vehicles (UAV) and drones.

--------
## Output
- Creates log files in three formats: kismet (SQLite database, PcapPpi (legacy pcap), and PcapNg (modern pcap)
- Modern pcap and kismet can contain multiple Data Link Types (DLT)
- Other tools may have issues with multiple DLTs

Convert PcapNg to regular Pcap:
```
tshark -F pcap -r ${pcapng file} -w ${pcap file}
```

Conf-file with centralized log directory, pcapng format and loopback-address:
```

log_prefix=/var/log/kismet/
log_types=kismet,pcapng
httpd_bind_address=127.0.0.1
```

----
## Running
```
sudo kismet -c wlan0
```
--no-ncurses for preserved terminal history

Specifying channels:
```
sudo kismet -c wlan0:channels="4,5,6"
```

Run in background as service:
```
sudo kismet --daemonize
```

Kill service:
```
ps -aux | grep kismet
kill -9 <pid>
```

------
## Remote Capture
- Allows for separate capture devices sending data to remote server

Server setup:
```
sudo kismet
```

Host setup:
```
#SSH forwarding local port 8000 to remote port:
ssh kali@192.168.62.192 -L 8000:localhost:3501

#Start capture and send to port 8000:
sudo kismet_cap_linux_wifi --connect 127.0.0.1:8000 --source=wlan0 -T <log-types> -p <log-prefix>
```
-n for no-logging and debugging purposes

Reading pcaps into Kismet:
```
sudo kismet -c file.pcap:realtime=true
```

Check datasources in kismet file:
```
kismetdb_to_pcap --in file.kismet --list-datasources
```

Convert kismet-files to Pcap and PcapNg:
```
kismetdb_to_pcap --in file.kismet --out file.pcapng --verbose
```

Convert kismet-file to JSON:
```
kismetdb_dump_devices --in /var/log/kismet/Kismet-20200917-17-45-17-1.kismet --out sample.json --skip-clean --verbose
```
