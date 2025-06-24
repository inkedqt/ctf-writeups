# 🛡️ Cyber Security Portfolio

Hi, I'm **Tate Pannam**, a cyber security student at Victoria University in Melbourne, Australia. This repository documents my journey through a variety of Hack The Box (HTB) challenges, including **retired**, **active**, and **seasonal** machines.

While I’ve completed a few retired boxes to reinforce foundational concepts and showcase progression, my primary focus has been on **seasonal** and **active** machines. These boxes present a greater challenge due to the lack of public writeups and require a deeper level of enumeration, exploitation, and problem-solving — making them far more valuable for real-world skill development.

Each machine listed includes a proof image, a direct link to my full writeup, and a concise summary to highlight the core techniques used.


---

## ✅ Retired HTB Machines

| Machine        | Difficulty | Status  | Proof                                                  | Writeup                                                                                                 | Summary                                                    |
|----------------|------------|---------|---------------------------------------------------------|---------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| Titanic     | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/titanic.png" style="width:50%;" />     | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Titanic)                         | LFI → SQLite → Gitea → ImageMagick identify RCE → root         |
| Administrator  | Medium     | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/administrator.png" style="width:50%;" />| [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Administrator)                    | AD domain takeover → Kerberoast → DCSync → Admin hash      |
| Beep           | Medium     | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/beep.png" style="width:50%;" />         | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Beep)                             | vtigerCRM LFI → legacy creds reuse → root via SSH          |
| Trick          | Medium     | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/trick.png" style="width:50%;" />        | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Trick)                            | DNS & SQLi → email RCE → fail2ban privesc                  |
| Waldo          | Medium     | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/waldo.png" style="width:50%;" />        | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Waldo)                            | LFI → SSH key → restricted shell escape → cap_dac_read     |
| Down           | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/down.png" style="width:50%;" />         | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Down)                             | LFI → command injection → pswm decrypt → sudo full root     |
| Lame           | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/lame.png" style="width:50%;" />         | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/lame)                             | Samba usermap exploit → SYSTEM shell                       |
| blue           | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/blue.png" style="width:50%;" />         | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/blue)                             | EternalBlue MS17-010 → SYSTEM shell                        |
| optimum        | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/optimum.png" style="width:50%;" />      | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/optimum)                          | Rejetto HFS RCE → SYSTEM with local tools                  |
| Bashed         | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/bashed.png" style="width:50%;" />       | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/Bashed)                           | Web fuzzing → PHP webshell → privesc via script abuse      |
| chemistry      | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/chemistry.png" style="width:50%;" />    | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/chemistry)                        | File parser RCE → LFI → SSH key reuse                      |
| headless       | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/headless.png" style="width:50%;" />     | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/headless)                         | Blind XSS → cookie theft → command injection → root        |
| alert          | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/alert.png" style="width:50%;" />        | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Retired/alert)                            | Markdown XSS → LFI → group permission privesc              |

---

## 🔒 Active HTB Machines this section is 🔒 private until the box retires. 🔒

| Machine     | Difficulty | Status  | Proof                                                  | Writeup                                                                                             | Summary                                                        |
|-------------|------------|---------|---------------------------------------------------------|-----------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| Dog         | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/dog.png" style="width:50%;" />         | [View](https://github.com/inkedqt/ctf-writeups/blob/main/HTB/Active/Dog)                             | Git repo dump → CMS RCE → PHP utility privilege escalation     |
| Code        | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/code.png" style="width:50%;" />        | [View](https://github.com/inkedqt/ctf-writeups/blob/main/HTB/Active/Code)                            | SQLi → MD5 crack → path traversal → SSH → root                 |
| Planning    | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/planning.png" style="width:50%;" />    | [View](https://github.com/inkedqt/ctf-writeups/blob/main/HTB/Active/Planning)                        | Subdomain → Grafana RCE → docker escape → SUID privesc        |
| Nocturnal   | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/nocturnal.png" style="width:50%;" />   | [View](https://github.com/inkedqt/ctf-writeups/blob/main/HTB/Active/Nocturnal)                       | File leak → admin panel RCE → DB hash → SSH → CVE → root      |
| Environment | Medium     | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/environment.png" style="width:50%;" /> | [View](https://github.com/inkedqt/ctf-writeups/blob/main/HTB/Active/Environment)                     | Laravel env bypass → avatar RCE → vault → sudo abuse          |

---

## 🗓️ Seasonal Boxes this section is 🔒 private until the box retires. 🔒

| Machine       | Difficulty | Status  | Proof                                                  | Writeup                                                                                             | Summary                                                              |
|---------------|------------|---------|---------------------------------------------------------|-----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| Artificial    | Easy       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/artificial.png" style="width:50%;" /> | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Seasonal/Artificial)                     | TensorFlow RCE via model → SQLite loot → MD5 crack → RESTIC trick → SUID bash root |
| Sorcery       | Insane     | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/sorcery.png" style="width:50%;" />     | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Seasonal/Sorcery)                         | Git leak → passkey bypass → Kafka RCE → Docker registry → IPA privesc |
| TombWatcher   | Hard       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/tombwatcher.png" style="width:50%;" /> | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Seasonal/Tombwatcher)                     | gMSA abuse → ACL pivot → deleted obj restore → CVE → Domain Admin   |
| Fluffy        | Hard       | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/fluffy.png" style="width:50%;" />      | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Seasonal/Fluffy)                          | NTLMv2 → shadow creds → ADCS ESC1 → Pass-the-Cert → Domain Admin    |
| Puppy         | Medium     | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/puppy.png" style="width:50%;" />       | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Seasonal/Puppy)                           | LDAP → KeePass → password reset → DPAPI secrets → NTDS.dit dump     |
| Certificate   | Medium     | ✅ Done | <img src="https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/certificate.png" style="width:50%;" /> | [View](https://github.com/inkedqt/ctf-writeups/tree/main/HTB/Seasonal/Certificate)                   | Cert template abuse → Certipy → Evil-WinRM → Administrator shell    |

---

📂 Proof images stored in: `/HTB/proofs/`  
📚 Writeups in: `/HTB/<Category>/<Box>/README.md`

*Maintained by [inksec](https://github.com/inkedqt)*

