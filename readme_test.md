# 🛡️ Cyber Security Portfolio

Hi, I'm **Tate Pannam**, a cyber security student at Victoria University in Melbourne, Australia. This repository documents my progression through a wide range of Hack The Box (HTB) challenges, including **retired**, **active**, and **seasonal** boxes.

Each machine listed includes a short summary, a proof image, and a direct link to my full writeup. This structure helps showcase my skills and serves as a reference for future engagements.

---

## ✅ Retired HTB Machines

| Machine        | Difficulty | Status  | Summary                                                    | Proof                                                  | Writeup                                                   |
|----------------|------------|---------|-------------------------------------------------------------|---------------------------------------------------------|------------------------------------------------------------|
| Lame           | Easy       | ✅ Done | Samba usermap exploit → SYSTEM shell                       | ![Lame](./status/proofs/lame.png)                      | [View](../HTB/Retired/Lame/README.md)                     |
| Blue           | Easy       | ✅ Done | EternalBlue MS17-010 → SYSTEM shell                        | ![Blue](./status/proofs/blue.png)                      | [View](../HTB/Retired/Blue/README.md)                     |
| Optimum        | Easy       | ✅ Done | Rejetto HFS RCE → SYSTEM with local tools                  | ![Optimum](./status/proofs/optimum.png)                | [View](../HTB/Retired/Optimum/README.md)                  |
| Bashed         | Easy       | ✅ Done | Web fuzzing → PHP webshell → privesc via script abuse      | ![Bashed](./status/proofs/bashed.png)                  | [View](../HTB/Retired/Bashed/README.md)                   |
| Beep           | Medium     | ✅ Done | vtigerCRM LFI → legacy creds reuse → root via SSH          | ![Beep](./status/proofs/beep.png)                      | [View](../HTB/Retired/Beep/README.md)                     |
| Administrator  | Medium     | ✅ Done | AD domain takeover → Kerberoast → DCSync → Admin hash      | ![Admin](./status/proofs/administrator.png)            | [View](../HTB/Retired/Administrator/README.md)           |
| Chemistry      | Easy       | ✅ Done | File parser RCE → LFI → SSH key reuse                      | ![Chemistry](./status/proofs/chemistry.png)            | [View](../HTB/Retired/Chemistry/README.md)                |
| Headless       | Easy       | ✅ Done | Blind XSS → cookie theft → command injection → root        | ![Headless](./status/proofs/headless.png)              | [View](../HTB/Retired/Headless/README.md)                 |
| Trick          | Medium     | ✅ Done | DNS & SQLi → email RCE → fail2ban privesc                  | ![Trick](./status/proofs/trick.png)                    | [View](../HTB/Retired/Trick/README.md)                    |
| Waldo          | Medium     | ✅ Done | LFI → SSH key → restricted shell escape → cap_dac_read     | ![Waldo](./status/proofs/waldo.png)                    | [View](../HTB/Retired/Waldo/README.md)                    |
| Alert          | Easy       | ✅ Done | Markdown XSS → LFI → group permission privesc              | ![Alert](./status/proofs/alert.png)                    | [View](../HTB/Retired/Alert/README.md)                    |

---

## 🔓 Active HTB Machines

| Machine     | Difficulty | Status  | Summary                                                        | Proof                                                  | Writeup                                                   |
|-------------|------------|---------|----------------------------------------------------------------|---------------------------------------------------------|------------------------------------------------------------|
| Titanic     | Easy       | ✅ Done | LFI → SQLite → Gitea → ImageMagick identify RCE → root         | ![Titanic](./status/proofs/titanic.png)                | [View](../HTB/Active/Titanic/README.md)                   |
| Dog         | Easy       | ✅ Done | Git repo dump → CMS RCE → PHP utility privilege escalation     | ![Dog](./status/proofs/dog.png)                        | [View](../HTB/Active/Dog/README.md)                       |
| Code        | Easy       | ✅ Done | SQLi → MD5 crack → path traversal → SSH → root                 | ![Code](./status/proofs/code.png)                      | [View](../HTB/Active/Code/README.md)                      |
| Planning    | Easy       | ✅ Done | Subdomain → Grafana RCE → docker escape → SUID privesc        | ![Planning](./status/proofs/planning.png)              | [View](../HTB/Active/Planning/README.md)                  |
| Nocturnal   | Easy       | ✅ Done | File leak → admin panel RCE → DB hash → SSH → CVE → root      | ![Nocturnal](./status/proofs/nocturnal.png)            | [View](../HTB/Active/Nocturnal/README.md)                 |
| Environment | Medium     | ✅ Done | Laravel env bypass → avatar RCE → vault → sudo abuse          | ![Environment](./status/proofs/environment.png)        | [View](../HTB/Active/Environment/README.md)               |

---

## 🗓️ Seasonal Boxes

| Machine       | Difficulty | Status  | Summary                                                              | Proof                                                  | Writeup                                                   |
|---------------|------------|---------|----------------------------------------------------------------------|---------------------------------------------------------|------------------------------------------------------------|
| TombWatcher   | Hard       | ✅ Done | gMSA abuse → ACL pivot → deleted obj restore → CVE → Domain Admin   | ![TombWatcher](./status/proofs/tombwatcher.png)        | [View](../HTB/Active/Tombwatcher/README.md)               |
| Fluffy        | Hard       | ✅ Done | NTLMv2 → shadow creds → ADCS ESC1 → Pass-the-Cert → Domain Admin    | ![Fluffy](./status/proofs/fluffy.png)                  | [View](../HTB/Active/Fluffy/README.md)                    |
| Puppy         | Medium     | ✅ Done | LDAP → KeePass → password reset → DPAPI secrets → NTDS.dit dump     | ![Puppy](./status/proofs/puppy.png)                    | [View](../HTB/Active/Puppy/README.md)                     |
| Certificate   | Medium     | ✅ Done | Cert template abuse → Certipy → Evil-WinRM → Administrator shell    | ![Certificate](./status/proofs/certificate.png)        | [View](../HTB/Active/Certificate/README.md)               |

---

📂 Proof images stored in: `/HTB/status/proofs/`  
📚 Writeups in: `/HTB/<Category>/<Box>/README.md`

*Maintained by [inksec](https://github.com/inkedqt)*

