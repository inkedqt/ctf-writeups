# 📊 Overwatch – HTB Seasonal

**Status:** 🔒 Private – writeup will be published once the machine retires  
**Difficulty:** Medium  
**Platform:** Windows  
**Category:** Active Directory | MSSQL | DNS Poisoning | WCF Exploitation

---

## 🧠 Teaser

Overwatch is a Windows domain controller that demonstrates how seemingly isolated components in enterprise infrastructure can be chained together to achieve full system compromise.

The box opens with guest SMB access revealing a .NET monitoring application. What appears to be a simple configuration leak quickly becomes the foundation for a multi-stage attack: hardcoded database credentials lead to MSSQL access, which in turn reveals a broken SQL Server linked server configuration. The real elegance lies in recognizing that the broken link isn't a dead end—it's an opportunity.

With Active Directory DNS write permissions, you can poison name resolution to intercept authentication attempts, capturing credentials that provide initial foothold access. From there, the privilege escalation vector centers on a localhost-bound WCF service running under SYSTEM. The challenge isn't just finding the service—it's understanding how to interact with SOAP-based Windows Communication Foundation endpoints without metadata, and exploiting a PowerShell command injection vulnerability hiding in plain sight.

Overwatch rewards methodical enumeration, understanding of Windows service architectures, and the ability to recognize when "service unavailable" actually means "exploit opportunity."

---

## 🪛 Tools You'll Want (High-Level)

```
🔍 SMB enumeration and file extraction
🧠 .NET decompilation skills (dnSpy)
💾 MSSQL client interaction (Impacket)
🌐 Active Directory DNS manipulation (bloodyAD)
🎯 MITM attack tooling (Responder)
📡 WCF/SOAP service interaction
💉 Understanding of command injection in scripting contexts
```

This box favors infrastructure knowledge over raw exploitation complexity.

---

## ✅ You'll Need To:

```
🗂️ Extract and analyze .NET application binaries from SMB shares
🔐 Recover hardcoded credentials from application configuration files
💾 Enumerate MSSQL linked server configurations
🌐 Exploit Active Directory DNS write permissions to poison name resolution
🎣 Capture cleartext credentials via MITM on poisoned DNS entries
🔧 Reverse engineer WCF service contracts without WSDL/MEX metadata
🧪 Craft SOAP requests to invoke remote methods
💉 Exploit PowerShell command injection in a Windows service
```

---

## 🧠 Takeaways

```
- Guest SMB access can leak application binaries containing hardcoded credentials
- Configuration files are treasure troves—they reveal architecture, credentials, and internal services
- MSSQL linked servers create trust relationships that can be weaponized
- Active Directory DNS write permissions enable powerful MITM attacks
- "Unreachable" services may just need DNS assistance to become very reachable
- WCF services can be reverse engineered from compiled .NET binaries when metadata is unavailable
- SOAP isn't just legacy—it's still running critical Windows infrastructure
- Command injection doesn't always need web forms—service endpoints work too
- Services running as SYSTEM under HTTP.sys (PID 4) are high-value privilege escalation targets
```

Overwatch is an excellent demonstration of enterprise Windows attack chains. It shows how credentials flow between systems, how DNS controls authentication, and how internal services become external attack surfaces when trust boundaries are crossed. The combination of AD enumeration, database pivoting, name resolution poisoning, and service exploitation makes this a comprehensive Windows infrastructure challenge.

---

## 📸 Proof

![Overwatch Proof](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/overwatch.png)