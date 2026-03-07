---
name: CCTV
difficulty: Easy
platform: Linux
status: ✅
---

## Summary
Default creds on ZoneMinder v1.37.63 → CVE-2024-51482 Boolean SQLi on tid parameter → 
credentials dumped from zm.Users table → SSH as mark → internal motionEye service on 
port 7999 → picture_filename command injection via on_picture_save → root shell.