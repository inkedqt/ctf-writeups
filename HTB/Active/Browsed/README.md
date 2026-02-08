# 📊 Browsed – HTB Seasonal

**Status:** 🔒 Private – writeup will be published once the machine retires  
**Difficulty:** Medium  
**Platform:** Linux  
**Category:** Web | Client-Side Attacks | Code Review | Privilege Escalation

---

## 🧠 Teaser

Browsed explores what happens when user-generated content isn't just stored—it's _executed_.

The box centers on a web application that allows users to submit Chrome browser extensions for review. But "review" here means something specific: a backend developer actually installs and tests your extension in their own browser. That workflow—where user-controlled code becomes trusted developer context—is the entire threat model.

From there, the box becomes a study in **chained browser-based exploitation**: reaching services that were never meant to be externally accessible, identifying implementation flaws in internal tooling, and finally pivoting from application-level access to full system control through configuration mistakes that seem small but prove critical.

---

## 🪛 Tools You'll Want (High-Level)

```
🌐 Understanding of browser extension architecture
🔍 Ability to review application source code for logic flaws
🧠 Familiarity with localhost/SSRF primitives
💉 Knowledge of shell interpreter edge cases
🐍 Python import mechanics and caching behavior
```

This box rewards understanding _execution context_ over raw exploitation skill.

---

## ✅ You'll Need To:

```
🎯 Recognize how browser extensions execute in privileged contexts
🔗 Chain client-side execution with server-side enumeration
📖 Perform source code review of internal services
🧪 Exploit subtle shell interpreter behaviors in comparison operators
🔐 Abuse Python's module caching system for privilege escalation
```

---

## 🧠 Takeaways

```
- Browser extensions are miniapplications with significant privilege—treat them as code execution vectors
- "Localhost-only" services become externally reachable when client contexts are compromised
- Shell arithmetic evaluation can execute commands even when input appears quoted and safe
- Python's bytecode caching can be weaponized when cache directories have weak permissions
- Attack surfaces often span multiple execution contexts (browser → localhost → filesystem → process)
```

Browsed is an excellent example of how modern web applications create complex trust boundaries—and how attackers navigate between them. It demonstrates that "client-side" and "server-side" are often false distinctions when execution contexts can be bridged.

## 📸 Proof

![Browsed Proof](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/HTB/proofs/browsed.png)