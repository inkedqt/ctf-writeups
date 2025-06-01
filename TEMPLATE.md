CTF Writeup Template (Hack The Box / TryHackMe / Custom)

🧪 Machine Name: MACHINE_NAME

Platform: Hack The Box / TryHackMe / OtherIP Address: IP_ADDRESSDifficulty: Easy / Medium / HardAuthor: YourNameDate: DD-MM-YYYY

🧭 Overview

Provide a high-level summary of the machine or challenge. What was the general flow? What skills were tested?

🔍 Enumeration

🔎 Nmap

nmap -p- MACHINE_NAME --min-rate 10000
nmap -p PORTS MACHINE_NAME -sCV -oN nmapscan

Open ports:

PORT/SERVICE - Info

🌐 Web Enumeration (if applicable)

Tools: gobuster / ffuf / manual testingFindings: Web titles, forms, upload points, JavaScript hints, cookies, etc.

⚙️ Initial Access

Method: Upload vuln / Web exploit / Weak creds / LFI / RCE / Buffer Overflow

Explain the vulnerability, exploit used, and payload:

Payload / Exploit / File contents / Curl command

Got shell as: USERNAME

🐚 Shell Stabilization

python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm-256color

Optionally: SSH forwarding, environment setup, stty fix

🔍 Post-Exploitation Enumeration

Look for config files, credentials, databases

Check /home, /var/www, custom binaries, crontab, etc.

🔐 User Privilege Escalation

Method: Password reuse / Sudo misconfig / Cron job / Capability / Kernel / LFI

Exploit steps or code used

Escalated to: NEWUSER

⬆️ Root Privilege Escalation

Method: Exploit / SSH key dump / LFI / Docker breakout / Capabilities / Sudo

Steps, file reads, or escalation commands

Got root via: METHOD

✅ Summary Table

Stage

Technique Used

Foothold



User Escalation



Root Access



🧠 Lessons Learned

Key takeaways and vulnerabilities abused

Good habits or tools discovered

Writeup by inksec GitHub: [https://github.com/inkedqt]