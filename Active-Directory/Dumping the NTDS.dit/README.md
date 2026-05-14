# Dumping the NTDS.dit – Active Directory Security Lab

![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-blue)
![Environment](https://img.shields.io/badge/Environment-VMware-orange)
![Focus](https://img.shields.io/badge/Focus-NTDS.dit-red)
![Tools](https://img.shields.io/badge/Tools-Impacket%20%7C%20Hashcat-green)
![Lab](https://img.shields.io/badge/Lab-TCM%20Security-success)
![License](https://img.shields.io/badge/License-Educational-lightgrey)

---

# Overview

This repository documents my hands-on learning experience during the **"Dumping the NTDS.dit"** phase of the TCM Security Active Directory lab.

The purpose of this lab is to understand:

- How Active Directory stores authentication data
- What the NTDS.dit database contains
- How domain credential extraction works in controlled environments
- Why NTLM hashes are highly sensitive
- The security impact of weak password policies
- Defensive awareness for enterprise Active Directory environments

All activities were performed strictly inside an isolated and authorized virtual lab environment for educational and defensive cybersecurity learning purposes.

---

# What is NTDS.dit?

`NTDS.dit` is the primary database used by Microsoft Active Directory Domain Services (AD DS).

It stores critical domain information including:

- User accounts
- Group information
- Security descriptors
- Authentication-related data
- NTLM password hashes

Because of this, NTDS.dit is considered one of the most sensitive components inside an Active Directory environment.

---

# Lab Environment

## Virtual Machines

- Kali Linux (Attacker Machine)
- Windows Domain-Joined Workstation
- Active Directory Domain Controller

## Technologies & Tools

- VMware
- Kali Linux
- Active Directory
- SMB
- Impacket Toolkit
- Hashcat
- Mimikatz
- CrackMapExec

---

# Topics Practiced

## Active Directory Enumeration

- SMB validation
- Domain communication checks
- Host discovery

## NTDS Interaction

- DRSUAPI method understanding
- Domain credential extraction concepts
- NTLM hash collection in a lab environment

## Offline Password Analysis

- Password auditing
- Dictionary-based testing
- Weak password identification

## Security Concepts Learned

- Domain compromise impact
- Password reuse risks
- Credential exposure dangers
- Privilege abuse awareness
- Defensive security considerations

---

# Sample Sanitized Commands

```bash
impacket-secretsdump DOMAIN/user:'PASSWORD'@X.X.X.X -just-dc-ntlm

hashcat -m 1000 hashes.txt /path/to/wordlist.txt
```

# Key Learning Outcomes

- Weak passwords significantly increase organizational risk
- NTLM hashes must be protected at all times
- Active Directory compromise can rapidly escalate
- Monitoring and segmentation are essential
- Strong password policies and MFA are critical defenses

# Important Notice

This repository DOES NOT contain:

- Real credentials
- Real password hashes
- Real IP addresses
- Sensitive configurations
- Production environment data
- Unauthorized access material

All sensitive values have been sanitized or replaced with placeholder data.

# Future Learning Goals

- Kerberoasting
- Pass-the-Hash concepts
- Lateral Movement
- BloodHound analysis
- Windows hardening
- Detection engineering
- Active Directory defense strategies

# Educational Disclaimer

This repository is intended strictly for:

- Cybersecurity education
- Ethical hacking training
- Defensive security awareness
- Authorized lab experimentation

Any misuse of the information contained here is strictly discouraged.

# Connect With Me

## GitHub

- https://github.com/bilalhunzla

## LinkedIn

- https://www.linkedin.com/in/hunzla-bilal
