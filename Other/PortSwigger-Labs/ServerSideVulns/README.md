
# PortSwigger Web Security Academy  
## Server-Side Vulnerabilities (Apprentice Path)

📚 [Link to Path](https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice)

---

## 🏆 Completed Labs

- ✅ Path Traversal
- ✅ Access Control
- ✅ Authentication
- ✅ Server-Side Request Forgery (SSRF)
- ✅ File Upload Vulnerabilities
- ✅ OS Command Injection
- ✅ SQL Injection

---

## 📖 Summary

The **Server-Side Vulnerabilities** path teaches essential web exploitation skills focusing on how to abuse server-side flaws to bypass controls, steal data, and gain code execution.

This path covers **critical real-world web attacks**, with each lab demonstrating a practical scenario.

---

## Lab Summaries

### 🗂 Path Traversal

- Using `../../../../etc/passwd` in image request parameters
- Basic path traversal to read sensitive files

---

### 🚪 Access Control

- Accessing hidden paths via `robots.txt`
- Security through obscurity bypass via DOM inspection revealing hidden admin panel
- Cookie tampering → setting `Admin=true`
- Insecure Direct Object Reference (IDOR) → changing `id` parameter to access another user's data

---

### 🔐 Authentication

- Intruder-based brute force username & password discovery
- Identifying valid username via response length
- Bypassing 2FA with forced navigation → changing URL after login step

---

### 🌐 Server-Side Request Forgery (SSRF)

- Modifying stock checking request: `stockApi=http://localhost/admin`
- Using SSRF to interact with internal services
- Brute forcing internal IP ranges with intruder (`192.168.0.X`)
- Using SSRF to perform sensitive actions (delete user Carlos)

---

### 📂 File Upload Vulnerabilities

- Uploading `.php` files to avatar field
- File content used:
  ```php
  <?php echo file_get_contents('/home/carlos/secret'); ?>
  ```
- Bypassing content-type validation:
  - Change `Content-Type` to `image/jpeg` to bypass checks
- Access uploaded PHP to execute on server

---

### ⚙️ OS Command Injection

- Using payloads such as:
  ```
  productId=1|whoami
  ```
- Executing system commands on server via unsanitized input
- Typical discovery flow:
  - `whoami`, `uname -a`, `netstat -an`, `ifconfig`, `ps -ef`

---

### 💥 SQL Injection (SQLi)

- Basic `OR 1=1` injection
- Subverting application logic:
  - Username → `administrator'--`
  - Bypass login checks
- Unreleased products enumeration via SQL injection in product category filter

---

## 🧠 Key Skills Learned

- Path Traversal → LFI variant
- IDOR (Insecure Direct Object Reference)
- Access Control Bypass (client-side controls, cookies, hidden endpoints)
- SSRF attacks → reaching internal services
- File Upload to RCE (Content-Type bypass tricks)
- Command Injection (POST parameter injection)
- SQL Injection → Login bypass, data leakage
- Brute-forcing usernames & passwords via Burp Intruder
- 2FA bypass → forced navigation / ID manipulation

---

## 🔭 Reflection

This is an excellent foundational web exploitation path.  
These skills are highly transferable to CTFs and real-world bug bounty:

✅ **Practical parameter tampering**  
✅ **SSRF workflows & IP brute**  
✅ **Modern IDOR understanding**  
✅ **File upload RCE techniques**  
✅ **OS Command Injection tricks**  
✅ **Path Traversal / LFI nuances**  
✅ **Authentication edge cases**  

---

*Writeup by inksec*  
GitHub: [https://github.com/inkedqt](https://github.com/inkedqt)
