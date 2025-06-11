
# Cyber Security portfolio
I'm Tate Pannam a cyber security student at VU in Melbourne Australia.

Welcome to my collection of CTF writeups and learning progress. This repo tracks boxes I've completed across various platforms including Hack The Box, HTB Academy, and others.

I want to document my learning progression and maintain a reference of commands and techniques used in completed boxes for future reference.

---

## 🚩 Featured Writeups

- 🔍 [HTB: Waldo](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Waldo)  
  LFI → Read SSH key → Rbash escape → Capabilities abuse (`cap_dac_read_search`) → Root flag via `tac`

- 🪄 [HTB: Trick](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Trick)  
  DNS & vHost discovery → SQLi + file read → LFI to RCE via email injection → PrivEsc with writable fail2ban config → Root shell

- 🏰 [HTB: Administrator](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Administrator)  
  Full Active Directory domain takeover via WinRM foothold → ACL abuse → password spraying → Kerberoast → DCSync → Administrator hash  

- 🧠 [HTB: Headless](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/headless)  
  Blind XSS in User-Agent header → Cookie theft → Command injection → Root via sudo script path hijack

- 🧪 [HTB: Chemistry](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/chemistry)  
  Remote file parsing → RCE via pymatgen, local file inclusion, and SSH key abuse

- 🛎️ [HTB: Alert](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/alert)  
  Advanced Markdown XSS → Base64 exfil → LFI → Group permission privesc

- 🧱 [HTB: Lame](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Lame)  
  Classic Linux box exploited via Samba usermap script (Metasploit)

- 💙 [HTB: Blue](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Blue)  
  EternalBlue exploit (MS17-010) on Windows 7, gaining full SYSTEM access

- ⚙️ [HTB: Optimum](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Optimum)  
  Rejetto HFS exploit + WinPEAS + local exploit suggester for SYSTEM shell

- 🌐 [PortSwigger: Server-Side Vulnerabilities](https://github.com/inkedqt/ctf-writeups/tree/main/Other/PortSwigger-Labs/ServerSideVulns)  
  Path Traversal • Access Control • IDOR • Auth bypass • SSRF • File Upload RCE • Command Injection • SQLi — common web vulns & practical exploitation.

- 🎓 [HTB Starting Point - Tier 0](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/StartingPoint/Tier0)  
  Meow • Fawn • Dancing • Redeemer • Explosion • Preignition • Mongod • Synced — foundational service enumeration, web fuzzing, password cracking & DB abuse.

- 🎓 [HTB Starting Point - Tier 1](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/StartingPoint/Tier1)  
  Appointment • Sequel • Crocodile • Responder • Three • Ignition • Bike • Funnel • Pennyworth • Tactics — web exploitation, SQLi, SMB attacks, Responder, priv esc & credential abuse.

- 🎓 [HTB Starting Point - Tier 2](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/StartingPoint/Tier2)  
  Archetype • Oopsie • Vaccine • Unified • Included • Markup • Base — SMB enumeration, file upload exploitation, JWT cracking, XXE injection, LFI, SUID privesc, advanced web enumeration & post-exploitation.

## Active Boxes
- 🚢 [HTB: Titanic (Active, Private Repo)](https://github.com/inkedqt/ctf-active/tree/main/HTB/Active/Titanic)  
  LFI on ticket download → SQLite DB dump → Gitea password hash crack → SSH as developer → ImageMagick identify RCE via cron → LD_PRELOAD SUID bypass → Root shell

### TombWatcher (Active Seasonal Box)

- 🗂️ [/HTB/Active/Tombwatcher/README.md](https://github.com/inkedqt/ctf-active/tree/main/HTB/Active/Tombwalker)  
📝 Windows AD box — gMSA abuse → ACL pivot → Deleted object restore → CVE-2024-49019 → Domain Admin  

Fluffy (Active Seasonal Box)  
- 🗂️ [/HTB/Active/Fluffy/README.md](https://github.com/inkedqt/ctf-active/tree/main/HTB/Active/Fluffy)  
📝 Windows AD box — NTLMv2 crack → Shadow Credentials abuse → ADCS certificate template enumeration → Certificate template abuse (ESC1) → Pass-the-Cert + Pass-the-Hash → Domain Admin  

Puppy (Seasonal Box)
- 🚀 [/HTB/Active/Puppy/README.md](https://github.com/inkedqt/ctf-active/tree/main/HTB/Active/Puppy)  
Medium Windows AD box — LDAP enumeration → SMB share access via group membership abuse → KeePass database password cracking → Password reset on disabled user → DPAPI credential extraction → Secretsdump for NTDS.dit extraction → Administrator NT hash → Evil-WinRM → U User + Root obtained  

---

## 🧰 Tools & Skills

### 🕵️ Discovery & Enumeration
`Nmap` `ffuf` `Gobuster` `Telnet` `FTP` `Redis` `MongoDB` `Rsync` `LDAP Enumeration` `BloodHound` `Responder`  
`SMB Enumeration` `SMB Relay` `SSH Enumeration` `SMB to WinRM flow` `LFI` `ffuf DNS bruteforce`  
`sqlite3 enumeration` `docker-compose parsing` `Flask app source review` `Kerberos Ticket Analysis` `Certificate Authority Enumeration`  
`rpcclient` `smbmap` `ldapsearch` `BloodHound-python` `LDAP enumeration and modification` `ntpdate (time sync for Kerberos)`  
`Kerberos ticket extraction via secretsdump` `KeePass4Brute` `KeePass database analysis`

### ⚔️ Exploitation
`SQL Injection` `Markdown XSS` `Base64 Exfiltration` `Reverse Shells` `File Upload Exploitation`  
`Credential Reuse` `Privilege Escalation` `Group Permission Abuse` `SUID Binaries` `CVE Hunting`  
`JWT Cracking` `XXE Injection` `Advanced LFI` `PBKDF2-SHA256 cracking (mode 10900)`  
`ImageMagick identify LD_PRELOAD abuse` `LD_PRELOAD bypass via .so hijack` `Systemd service discovery`  
`Shadow Credentials Abuse` `ADCS Certificate Template Abuse (ESC1/ESC13)` `Pass-the-Cert` `Pass-the-Hash`  
`Kerberos Ticket Caching & Reuse` `LDAP userAccountControl modification (enabling disabled accounts)`  
`Password spraying with credential lists` `Group membership abuse (bloodyAD)` `Impacket Secretsdump for NTDS.DIT extraction`  
`DPAPI masterkey and credential blob extraction` `Password recovery from KeePass DB` `Evil-WinRM with NT hash login`

### 🛠️ Post-Exploitation & Tools
`Burp Suite` `Python` `PHP` `SQLite` `Metasploit` `WinPEAS` `Local Exploit Suggester`  
`SMB Hash Cracking` `Password Cracking` `Zip Cracking` `EternalBlue` `Rejetto HFS`  
`gitea2hashcat` `Gitea DB extraction` `sqlite3` `getcap` `setcap` `gcc -fPIC -shared`  
`LD_PRELOAD` `Systemd .service analysis` `Certipy` `BloodyAD` `Evil-WinRM` `Impacket-Secretsdump`  
`Impacket-smbserver` `Impacket-DPAPI tools` `KeePassXC GUI` `ldapmodify` `BloodHound-python` `bloodyAD` `evil-winrm`



---

*Maintained by inksec / [GitHub](https://github.com/inkedqt)*
