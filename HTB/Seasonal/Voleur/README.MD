🛡️ Voleur (HTB Seasonal) Write up locked until box is retired as per HTB rules

Status: ✅ Writeup Published  
Difficulty: Medium  
Category: Active Directory | Windows | Kerberos | DPAPI  
Date Completed: 2025-07-12  

🧠 Teaser

A corporate domain with overlapping permissions, archived secrets, and one very persistent backup team...

Can you recover forgotten accounts, pry open DPAPI vaults, and turn legacy infrastructure into Domain Admin?

🪛 Bring your favorite tools:

    🩸 BloodHound
    🧪 dpapi.py
    🔍 netexec + smbclient.py
    📦 msoffcrypto-tool + office2john
    ⚙️ secretsdump.py, getTGT.py

You'll need to:

    Recover deleted users with AD recycle bin ♻️  
    Extract service account passwords from protected spreadsheets 🔐  
    Decrypt credential blobs with masterkeys 🗝️  
    Discover SSH access buried deep in backup systems 📁  
    Dump NTDS and impersonate the domain’s top dog 💼

📸 Proof  
![Voleur Proof](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/voleur.png)
