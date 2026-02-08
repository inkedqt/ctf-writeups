# 📊 AirTouch – HTB Seasonal

**Status:** 🔒 Private – writeup will be published once the machine retires  
**Difficulty:** Medium  
**Platform:** Linux  
**Category:** Network Security | Wireless Exploitation | Multi-VLAN Pivoting | Authentication Bypass

---

## 🧠 Teaser

AirTouch is a masterclass in wireless network exploitation and VLAN pivoting that simulates a realistic corporate WiFi infrastructure.

The box begins with network reconnaissance through an unconventional protocol, leading to initial access on a segmented consultant network. From there, the challenge becomes navigating a multi-tiered wireless architecture: consumer-grade WPA2-PSK networks, enterprise 802.1X authentication, and isolated VLANs that require creative pivoting techniques.

What makes AirTouch particularly engaging is its realistic simulation of corporate wireless security. You'll encounter the same authentication mechanisms, network segmentation, and trust boundaries that exist in real enterprise environments—and exploit the same weaknesses that make wireless networks a persistent attack vector.

The path to root requires chaining together wireless credential harvesting, man-in-the-middle attacks against enterprise authentication, and leveraging misconfigurations in network access control. It's not just about breaking WiFi—it's about understanding how wireless networks integrate with broader infrastructure and where those integration points fail.

---

## 🪛 Tools You'll Want (High-Level)

```
📡 Wireless security toolkit familiarity (aircrack-ng suite)
🔍 SNMP enumeration experience
🧠 Understanding of WPA2-PSK vs WPA2-Enterprise authentication
🎯 Man-in-the-middle attack concepts (evil twin/rogue AP)
🔑 Knowledge of EAP methods (PEAP, MSCHAPv2)
🌐 Network pivoting and multi-VLAN navigation
```

This box rewards wireless security knowledge and methodical network enumeration.

---

## ✅ You'll Need To:

```
🔎 Leverage SNMP information disclosure for initial access
📶 Perform WPA2-PSK handshake capture and offline cracking
🚀 Pivot across isolated network segments via wireless interfaces
🎭 Execute evil twin attacks against WPA2-Enterprise networks
🔓 Harvest and crack MSCHAPv2 challenge/response hashes
📋 Extract credentials from wireless authentication databases
🔐 Chain credential reuse across network tiers
```

---

## 🧠 Takeaways

```
- SNMP can leak far more than system information—including credentials
- WPA2-PSK remains vulnerable to offline dictionary attacks when handshakes are captured
- Network segmentation only works if all boundaries are properly enforced
- WPA2-Enterprise authentication can be compromised through rogue access points
- MSCHAPv2 challenge/response exchanges are crackable offline
- Configuration files for wireless infrastructure often contain plaintext credentials
- Certificate trust is critical—clients will authenticate to convincing rogue APs
- Multi-VLAN environments create complex but exploitable attack surfaces
```

AirTouch demonstrates that wireless security is only as strong as its weakest authentication mechanism. It's a realistic simulation of how attackers traverse segmented wireless networks, harvest credentials from over-the-air authentication, and exploit trust relationships between network tiers. For anyone interested in wireless penetration testing, this box covers essential techniques used in real-world engagements.

---

## 📸 Proof

![AirTouch Proof](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/airtouch.png)