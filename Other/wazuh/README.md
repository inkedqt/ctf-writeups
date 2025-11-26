# 🛡️ InkSec Lab: Wazuh + Sysmon Detection Walkthrough  
*Practical SIEM Deployment & Endpoint Telemetry*

---

# 1️⃣ Overview  
This lab demonstrates deploying a full **Wazuh SIEM** on Ubuntu and integrating a **Windows 11 endpoint** enhanced with **Sysmon** to generate high-quality security events.

The goal is to prove:

- Wazuh Manager is installed and running  
- Windows Agent is registered  
- Sysmon is installed  
- Security alerts + telemetry are flowing  
- File Integrity Monitoring (FIM) and inventory work

---

# 2️⃣ Environment  
- **Ubuntu Server** – Wazuh Manager  
- **Windows 11** – Wazuh Agent + Sysmon  
- Same NAT/bridged network  

---

# 3️⃣ Install Wazuh Manager (Ubuntu)

Install command:

```
curl -sO https://packages.wazuh.com/4.x/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

---

# 4️⃣ Access the Wazuh Dashboard

### 📸 Screenshot: Dashboard login screen  
![Dashboard Login](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot2.png)

Browse to:  
`https://<manager-ip>:55000`

### 📸 Screenshot: Dashboard home after login  
![Dashboard Home](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot3.png)

---

# 5️⃣ Register Windows Agent

### 📸 Screenshot: Windows agent GUI with manager IP + running status  
![Agent GUI](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot4.png)

Generated key from Wazuh UI → Agents → Deploy new agent.

Register via GUI or CLI:

```
"C:\Program Files (x86)\ossec-agent\agent-auth.exe" -m <manager-ip> -k "<auth-key>"
```

Restart agent service after registration.

---

# 6️⃣ Verify Agent Appears in Dashboard

### 📸 Screenshot: Agent list showing “win11 – Active”  
![Agent Active](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot5.png)

You should see:

- Status: **Active**  
- Version: 4.7.x  
- IP Address  
- Last Keep Alive timestamp  

---

# 7️⃣ Install Sysmon

Sysmon adds deep visibility: process creation, network connections, registry changes, etc.

Install:

```
Sysmon64.exe -accepteula -i sysmonconfig.xml
```

### 📸 Screenshot: Sysmon installed
![Sysmon Installed](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot6.png)

---

# 8️⃣ Validate Sysmon Events in Wazuh

Use the Discover tab or Security Events:

`rule.groups: "windows_sysmon"`

### 📸 Screenshot: Sysmon events showing (ProcessCreate, NetworkConnect, etc.)  
![Sysmon Events](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot7.png)

This proves end-to-end log ingestion works.

---

# 9️⃣ File Integrity Monitoring (FIM)

Modify a file inside a monitored path, e.g.:

```
C:\Windows\System32\drivers\etc\hosts
```

### 📸 Screenshot: FIM alert (“File integrity checksum changed”)  
![FIM Alert](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot8.png)

---

# 🔟 System Inventory (Syscollector)

Shows:

- Installed applications  
- Running services  
- Hardware  
- OS info

### 📸 Screenshot: Syscollector inventory page  
![Syscollector Inventory](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot9.png)

---

# 1️⃣1️⃣ Security Alerts

Trigger normal Windows activity or intentional Sysmon noise.

### 📸 Screenshot: Security alerts panel with agent name “win11”  
![Security Alerts](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/wazuh/img/screenshot10.png)

This proves correlation + rule matching is functioning.

---

# ✅ Conclusion

This lab shows complete SIEM deployment and endpoint visibility:

- Wazuh Manager installed  
- Windows agent enrolled  
- Sysmon telemetry active  
- File integrity monitoring operational  
- Alerts flowing in real time  
- Full system inventory collected  

This meets SIEM fundamentals and forms a strong foundation for further labs, including log parsing, custom rules, Active Response, and threat hunting.

---

