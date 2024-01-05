---
{"dg-publish":true,"permalink":"/oscp-playbook/"}
---

-----------------
## 1. Host Enumeration

#### 1.1. Passive Enumeration
- [[1. OSCP/1. Information Gathering/1. Passive Gathering#Whois Enumeration\|Whois]]
- [[1. OSCP/1. Information Gathering/1. Passive Gathering#Netcraft\|Netcraft]]
- [[1. OSCP/1. Information Gathering/1. Passive Gathering#Whatweb\|Whatweb]]
- [[1. OSCP/1. Information Gathering/1. Passive Gathering#Open-Source Code\|Github Leakage]]
	- gitrob
	- gitleaks
- [[1. OSCP/1. Information Gathering/1. Passive Gathering#Security Headers\|Security Headers]]
	- securityheaders.com
	- ssllabs.com\/ssltest
- [[1. OSCP/1. Information Gathering/1. Passive Gathering#Shodan\|Shodan]]
#### 1.2. Active Enumeration
- [[1. OSCP/1. Information Gathering/2. Active Gathering#DNS Enumeration\|DNS Enumeration]]
	- host
	- dnsrecon
	- dnsenum
	- nslookup (WIN)
- [[1. OSCP/1. Information Gathering/2. Active Gathering#Nmap\|Host Enumeration]]
	- nmap
	- Test-NetConnection (WIN)
	- nc
- [[1. OSCP/1. Information Gathering/3. SMB Enumeration\|SMB Enumeration]]
	- nbtscan
	- smbmap
	- net view (WIN)
	- CrackMapExec
- [[1. OSCP/1. Information Gathering/4. SMTP Enumeration\|SMTP Enumeration]]
	- nc
	- TelnetClient (WIN)
- [[1. OSCP/1. Information Gathering/5. SNMP Enumeration\|SNMP Enumeration]]
	- onesixtyone
	- snmpwalk
------------------
## 2. Vulnerability Scanning

- [[1. OSCP/2. Vulnerability Scanning/2. Nessus\|Nessus]]
- [[1. OSCP/2. Vulnerability Scanning/3. Nmap Scripting Engine\|NSE]]
----------------------
## 3. Web

#### 3.1. Web Application Enumeration
- [[1. OSCP/3. Web Applications/2.  Web Application Assessment#Nmap\|Banner Grabbing]]
	- nmap
	- nc
- [[1. OSCP/3. Web Applications/2.  Web Application Assessment#Directory busting\|Directory Busting]]
	- gobuster
	- dirb
	- dirsearch
- Source-code & Requests
	- burp
	- curl
- [[1. OSCP/3. Web Applications/2.  Web Application Assessment#Wappalyzer\|Infrastructure]]
- [[1. OSCP/3. Web Applications/3. Web Application Enumeration#Response-headers\|Response-headers]]
- [[1. OSCP/3. Web Applications/3. Web Application Enumeration#Sitemaps\|Sitemaps]]
- [[1. OSCP/3. Web Applications/3. Web Application Enumeration#API Enumeration\|API Fuzzing]]
- [[1. OSCP/3. Web Applications/3. Web Application Enumeration#Wordpress Enumeration\|Wordpress Enumeration]]
	- wpscan
	- dirsearch
- [[1. OSCP/1. Information Gathering/1. Passive Gathering#Netcraft\|Netcraft]]
- [[1. OSCP/1. Information Gathering/1. Passive Gathering#Whatweb\|Whatweb]]
#### 3.2. Web Application Attacks
- [[1. OSCP/3. Web Applications/5. Web Application Attacks#Cross-site-scripting (XSS)\|Cross-site-scripting]]
	- Stored XSS
	- Reflected XSS
	- DOM-based XSS
- [[1. OSCP/3. Web Applications/5. Web Application Attacks#Directory Traversal\|Directory Traversal]]
- [[1. OSCP/3. Web Applications/5. Web Application Attacks#Local File Inclusion (LFI)\|Local File Inclusion (LFI)]]
- [[1. OSCP/3. Web Applications/5. Web Application Attacks#Remote File Inclusion (RFI)\|Remote File Inclusion (RFI)]]
- [[1. OSCP/3. Web Applications/5. Web Application Attacks#PHP Wrappers\|PHP Wrappers]]
- [[1. OSCP/3. Web Applications/5. Web Application Attacks#File Upload\|File Upload]]
- [[1. OSCP/3. Web Applications/5. Web Application Attacks#OS Command Injection\|OS Command Injection]]
- [[1. OSCP/3. Web Applications/5. Web Application Attacks#SQL Injection\|SQL Injection]]
	- Error-based SQLi
	- Union-based SQLi
	- Blind SQLi
	- sqlmap
- [[MISC#WordPress-login Shell\|Wordpress Reverse Shell]]
---------
## 4. Client-side

#### 4.1. Target Reconnaissance
- [[1. OSCP/4. Client-side/1. Target Reconnaissance#Metadata\|Metadata leakage]]
- [[1. OSCP/4. Client-side/1. Target Reconnaissance#Tracking Tokens\|Canary tokens]]
#### 4.2. Client-side Attacks
- [[1. OSCP/4. Client-side/2. Client-side Attacks#Macros\|Macros]]
- [[1. OSCP/4. Client-side/2. Client-side Attacks#Windows Library Files\|Windows Library-ms]]
- Phishing
	- [[1. OSCP/4. Client-side/2. Client-side Attacks#SendEmail\|SendEmail]]
	- [[1. OSCP/4. Client-side/2. Client-side Attacks#Swaks\|Swaks]]
-------
## 5. Exploits

- [[1. OSCP/5. Public Exploits/2. Offline Exploit Resources#SearchSploit\|Exploit-DB/searchsploit]]
- [[1. OSCP/5. Public Exploits/1. Online Exploit Resources#Packet Storm\|Packet Storm]]
- [[1. OSCP/5. Public Exploits/1. Online Exploit Resources#GitHub\|GitHub]]
- [[1. OSCP/5. Public Exploits/1. Online Exploit Resources#Google\|Google]]
- [[1. OSCP/5. Public Exploits/2. Offline Exploit Resources#Exploit Frameworks\|Metasploit]]
- [[1. OSCP/5. Public Exploits/2. Offline Exploit Resources#Nmap NSE Scripts\|NSE Scripts]]
- Cross-compiling
	- [[1. OSCP/5. Public Exploits/3. Fixing Buffer Exploits\|mingw]]
--------
## 6. Anti-virus Evasion

#### 6.1. Evasion Testing
- [[1. OSCP/6. Antivirus Evasion/1. Testing for AV Evasion\|AntiScan.Me]]
- VirusTotal
#### 6.2. Evasion TTPs
- [[1. OSCP/6. Antivirus Evasion/2. Manual Thread Injection#One-liner genom encodedCommand\|Encoded PowerShell]]
- [[1. OSCP/6. Antivirus Evasion/2. Manual Thread Injection#In-memory Thread Injection Using Powershell\|PowerShell Thread Injection]]
- [[1. OSCP/6. Antivirus Evasion/3. Automatic PE Injection#Shellter Injection\|Shellter PE Injection]]
- [[1. OSCP/6. Antivirus Evasion/3. Automatic PE Injection#Veil AV Evasion\|Veil Payload Evasion]]
--------
## 7. Password Attacks

#### 7.1. Remote Password Attacks
- [[1. OSCP/7. Password Attacks/1. SSH & RDP Attacks#SSH Password Brute Force\|SSH/RDP Bruteforce]]
- [[1. OSCP/7. Password Attacks/1. SSH & RDP Attacks#RDP Password Spray\|Password-spray]]
- HTTP Login
	- [[1. OSCP/7. Password Attacks/2. HTTP Login Attack#HTTP-POST Attack\|HTTP-POST Attack]]
	- [[1. OSCP/7. Password Attacks/2. HTTP Login Attack#HTTP-GET Attack\|HTTP-GET Attack]]
#### 7.2. Hash-stealing
- [[1. OSCP/7. Password Attacks/5. Mimikatz#Mimikatz Usage\|Mimikatz]]
- Pass-the-hash
	- [[1. OSCP/7. Password Attacks/6. Pass-the-Hash#PtH Attack with SMBClient\|smbclient]]
	- [[1. OSCP/7. Password Attacks/6. Pass-the-Hash#PtH Attack with PSExec\|PSExec]]
	- [[1. OSCP/7. Password Attacks/6. Pass-the-Hash#PtH Attack with WMIExec\|WMIExec]]
- [[1. OSCP/7. Password Attacks/7. Net-NTLMv2 Stealing\|NTLMv2 Stealing]]
- [[1. OSCP/7. Password Attacks/8. Net-NTLMv2 Relaying\|NTLMv2 Relaying]]
#### 7.3. Hash-cracking
- Hash Enumeration
	- [[1. OSCP/7. Password Attacks/4. KeePass & SSH-key Crack#John hash-cracking\|hashid]]
	- [[1. OSCP/7. Password Attacks/4. KeePass & SSH-key Crack#John hash-cracking\|hash-identifier]]
- Hash Conversion
	- [[1. OSCP/7. Password Attacks/4. KeePass & SSH-key Crack#KeePass Hash Crack\|keepass2john]]
	- [[1. OSCP/7. Password Attacks/4. KeePass & SSH-key Crack#SSH-key Crack\|ssh2john]]
	- [[MISC#Crack zip-file with John\|zip2john]]
- Hash Cracking
	- [[1. OSCP/7. Password Attacks/3. Hash-cracking#Rule-based Attacks\|hashcat]]
	- [[1. OSCP/7. Password Attacks/4. KeePass & SSH-key Crack#John hash-cracking\|john]]
---------
## 8. Windows Privilege Escalation

#### 8.1. Enumeration
- [[1. OSCP/8. Windows Privilege Escalation/2. System Awareness\|System Awareness]]
- [[1. OSCP/8. Windows Privilege Escalation/3. Finding Secrets\|Finding Secrets]]
- [[1. OSCP/8. Windows Privilege Escalation/4. PowerShell Logs\|Powershell Logs]]
#### 8.2. Privilege Escalation
- [[1. OSCP/8. Windows Privilege Escalation/9. Using Exploits#Named Pipes\|Named Pipes (whoami /priv)]]
	- PrintSpoofer
- [[1. OSCP/8. Windows Privilege Escalation/10. Dumping SAM\|Dumping SAM]]
- [[1. OSCP/8. Windows Privilege Escalation/5. Service Hijacking#Writable Files + Directories\|Writable Files & Directories]]
- [[1. OSCP/8. Windows Privilege Escalation/5. Service Hijacking\|Service Binary Hijacking]]
- [[1. OSCP/8. Windows Privilege Escalation/7. Unquoted Service Paths\|Unquoted Service Paths]]
- [[1. OSCP/8. Windows Privilege Escalation/8. Scheduled Tasks\|Scheduled Tasks]]
- [[1. OSCP/8. Windows Privilege Escalation/6. DLL Hijacking\|DLL Hijacking]]
- [[1. OSCP/8. Windows Privilege Escalation/9. Using Exploits#Meterpreter UAC bypass\|UAC Bypass]]
- [[1. OSCP/7. Password Attacks/7. Net-NTLMv2 Stealing\|NTLMv2 Stealing]]
- [[1. OSCP/7. Password Attacks/8. Net-NTLMv2 Relaying\|NTLMv2 Relaying]]
------------
## 9. Linux Privilege Escalation

#### 9.1. Enumeration
- [[1. OSCP/9. Linux Privilege Escalation/2. Manual Enumeration#System awareness\|System Awareness]]
- [[1. OSCP/9. Linux Privilege Escalation/4. Exposed Information\|Finding Secrets + Logs]]
#### 9.2. Privilege Escalation
- [[1. OSCP/9. Linux Privilege Escalation/6. Insecure System Components#Sudo\|Sudo -l]]
- [[1. OSCP/9. Linux Privilege Escalation/6. Insecure System Components#SUID\|SUID Binaries]]
- [[1. OSCP/9. Linux Privilege Escalation/6. Insecure System Components#Capabilities\|Capabilities]]
- [[1. OSCP/9. Linux Privilege Escalation/2. Manual Enumeration#Writable directories & files\|Writable Files & Directories]]
	- [[1. OSCP/9. Linux Privilege Escalation/5. Insecure File Permissions#Abusing /etc/passwd\|Abusing /etc/passwd]]
- [[1. OSCP/9. Linux Privilege Escalation/5. Insecure File Permissions#Abusing Cronjobs\|Cronjobs]]
- [[1. OSCP/9. Linux Privilege Escalation/6. Insecure System Components#Kernel\|Exploits]]
	- PwnKit
	- Dirtypipes
	- Samedit
-----
## 10. Port Tunneling & Pivoting

#### 10.1. Linux Pivoting
- [[1. OSCP/10. Port Redirection & Tunneling/1. Linux Port Forwarding#Socat port forwarding\|Socat]]
- [[1. OSCP/10. Port Redirection & Tunneling/1. Linux Port Forwarding#Tunneling Theory + SOCKS\|Proxychains (SOCKS)]]
- [[1. OSCP/10. Port Redirection & Tunneling/6. Ligolo-ng\|Ligolo-ng]]
- SSH Port Forwarding
	- [[1. OSCP/10. Port Redirection & Tunneling/1. Linux Port Forwarding#SSH Local Port Forwarding\|Local PF]]
	- [[1. OSCP/10. Port Redirection & Tunneling/1. Linux Port Forwarding#SSH Dynamic Port Forwarding\|Dynamic PF]]
	- [[1. OSCP/10. Port Redirection & Tunneling/1. Linux Port Forwarding#SSH Remote Port Forwarding\|Remote PF]]
	- [[1. OSCP/10. Port Redirection & Tunneling/1. Linux Port Forwarding#SSH Remote Dynamic Port Forwarding\|Remote Dynamic PF]]
	- [[1. OSCP/10. Port Redirection & Tunneling/1. Linux Port Forwarding#SSHuttle\|SSHuttle Tunnel]]
#### 10.2. Windows Pivoting
- [[1. OSCP/10. Port Redirection & Tunneling/2. Windows Port Forwarding#SSH Remote Dynamic Port Forwarding\|SSH Remote Dynamic PF]]
- [[1. OSCP/10. Port Redirection & Tunneling/2. Windows Port Forwarding#Plink.exe Remote Port Forwarding + RDP binding\|Plink.exe Remote PF + RDP Binding]]
- [[1. OSCP/10. Port Redirection & Tunneling/2. Windows Port Forwarding#Netsh local port forwarding + firewall poking\|Netsh Local PF + Firewall Poking (Admin)]]
#### 10.3. Other Tunnels
- [[1. OSCP/10. Port Redirection & Tunneling/3. HTTP Tunneling\|Chisel HTTP Tunneling]]
- [[1. OSCP/10. Port Redirection & Tunneling/4. DNS Tunneling#DNS Tunneling with dnscat2\|DNScat2 DNS Tunneling]]
- [[1. OSCP/10. Port Redirection & Tunneling/5. Meterpreter Port Forwarding\|Automatic Metasploit PF]]
-------------
## 11. Metasploit Framework

- [[1. OSCP/11. Metasploit Framework/1. MSF Setup\|Setup]] 
- [[1. OSCP/11. Metasploit Framework/2. Meterpreter\|Meterpreter]]
- [[1. OSCP/11. Metasploit Framework/3. MSFVenom\|MSFVenom]]
- [[1. OSCP/11. Metasploit Framework/7. Automated Resource Scripts\|Automated Resource Scripts]]
- Post Exploitation
	- [[1. OSCP/11. Metasploit Framework/5. Meterpreter Post-Exploitation#Getsystem\|Meterpreter Getsystem]]
	- [[1. OSCP/11. Metasploit Framework/5. Meterpreter Post-Exploitation#Process Tampering\|Meterpreter Process Tampering]]
	- [[1. OSCP/11. Metasploit Framework/6. Post-Exploitation Modules#UAC bypass\|UAC Bypass Module]]
	- [[1. OSCP/11. Metasploit Framework/6. Post-Exploitation Modules#Kiwi Credential\|Meterpreter Kiwi Credential Dump]]
--------
## 12. Active Directory

#### 12.1 Enumeration
- [[1. OSCP/12. Active Directory Enumeration/1. Manual Enumeration\|net user]]
- [[1. OSCP/12. Active Directory Enumeration/2. Theory + LDAP Script\|LDAP]]
- [[1. OSCP/12. Active Directory Enumeration/3. PowerView Enumeration\|PowerView]]
- [[1. OSCP/12. Active Directory Enumeration/3. PowerView Enumeration\|PSLoggedOn]]
- [[1. OSCP/12. Active Directory Enumeration/7. BloodHound\|Bloodhound]]
#### 12.2. Manipulation & Escalation
- [[1. OSCP/13. Active Directory Attacks/4. Kerberoasting\|Kerberoasting]]
- [[1. OSCP/13. Active Directory Attacks/3. AS-REP Roasting\|ASREP Roasting]]
- [[1. OSCP/12. Active Directory Enumeration/4. Service Principal Names\|SPNs]] + [[1. OSCP/13. Active Directory Attacks/5. Silver Tickets\|Silver Tickets]]
- [[1. OSCP/12. Active Directory Enumeration/5. Object Permissions\|Object Permissions (GenericAll)]]
- [[1. OSCP/13. Active Directory Attacks/1. Theory + Mimikatz\|Lsass]]
- [[1. OSCP/12. Active Directory Enumeration/6. Domain Shares\|Domain Shares]]
- [[1. OSCP/13. Active Directory Attacks/6. DCSync Attack\|DCSync]]
- [[1. OSCP/14. Active Directory Movement/6. DCOM\|DCOM]]
- [[1. OSCP/7. Password Attacks/7. Net-NTLMv2 Stealing\|NTLMv2 Stealing]]
- [[1. OSCP/7. Password Attacks/8. Net-NTLMv2 Relaying\|NTLMv2 Relaying]]
#### 12.3. Authentication Manipulation
- [[1. OSCP/14. Active Directory Movement/3. Pass-the-Hash#Theory\|Pass-the-Hash]]
	- SMB
		- [[1. OSCP/1. Information Gathering/3. SMB Enumeration#SMBMap\|SMBMap]]
		- [[1. OSCP/7. Password Attacks/6. Pass-the-Hash#PtH Attack with SMBClient\|SMBClient]]
		- [[1. OSCP/1. Information Gathering/3. SMB Enumeration#CrackMapExec\|CME]]
	- [[1. OSCP/7. Password Attacks/6. Pass-the-Hash#PtH NT_AUTHORITY Shell with PSExec\|PsExec]]
	- [[1. OSCP/7. Password Attacks/6. Pass-the-Hash#PtH User Shell with WMIExec\|WMIExec]]
	- [[1. OSCP/7. Password Attacks/6. Pass-the-Hash#PtH with Evil-WinRM\|WinRM]]
	- [[1. OSCP/7. Password Attacks/6. Pass-the-Hash#PtH with Mimikatz\|Mimikatz]]
	- [[MISC#Linux RDP\|xfreeRDP]]
	- [[1. OSCP/13. Active Directory Attacks/4. Kerberoasting\|Kerberoasting]] & [[1. OSCP/13. Active Directory Attacks/3. AS-REP Roasting\|ASREP Roasting]]
- [[1. OSCP/14. Active Directory Movement/4. Overpass-the-Hash\|Overpass-the-Hash (Mimikatz)]]
- [[1. OSCP/14. Active Directory Movement/5. Pass-the-Ticket\|Pass-the-Ticket (Mimikatz)]]
#### 12.4. Credential Spraying
- [[1. OSCP/13. Active Directory Attacks/2. Password Attacks#SMB Password Attack with crackmapexec\|SMB Spray (crackmapexec)]]
- LDAP
	- [[1. OSCP/13. Active Directory Attacks/2. Password Attacks#Manual LDAP Password Attack\|Manual LDAP Spray]]
	- [[1. OSCP/13. Active Directory Attacks/2. Password Attacks#Automatic LDAP Attack with Spray-Passwords\|Automatic LDAP Spray (spray-passwords)]]
- [[1. OSCP/13. Active Directory Attacks/2. Password Attacks#Kerberos TGT Attack with kerbrute\|Kerberos TGT Spray]]
#### 12.5. Movement:
- [[MISC#Linux RDP\|RDP]]
- SSH
- [[1. OSCP/14. Active Directory Movement/1. WMI and WinRM#WMI\|WMI]]
- [[1. OSCP/14. Active Directory Movement/1. WMI and WinRM#WinRM\|WinRM]]
- [[1. OSCP/14. Active Directory Movement/2. PsExec\|PsExec]]
- [[MISC#Remote PS-Session as Domain Admin\|PSSession]]
------------------------
