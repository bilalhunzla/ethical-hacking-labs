# Active Directory Attack Chain – LLMNR to Lateral Movement

## 📌 Overview

This lab demonstrates a full attack chain starting from LLMNR poisoning to credential compromise, followed by password spraying, credential dumping, hash cracking, and lateral movement across multiple systems.

---

## 🎯 Objectives

- Capture credentials using LLMNR poisoning
- Crack captured hashes
- Perform password spraying
- Dump credentials using secretsdump
- Identify password reuse patterns
- Perform Pass-the-Hash
- Achieve lateral movement

---

## 🧪 Lab Setup

- Domain: MARVEL.local
- Attacker Machine: Kali Linux
- Target Machines:
  - Windows Client 1
  - Windows Client 2
  - Domain Controller

---

## ⚔️ Attack Steps

### 1. LLMNR Poisoning

Captured NTLM hash for a domain user.

---

### 2. Password Cracking

Recovered weak password from captured hash:

```
[REDACTED_PASSWORD]
```

---

### 3. Password Spraying

Used recovered credentials across multiple systems and identified valid logins.

---

### 4. Credential Dumping

Used:

```
impacket-secretsdump
```

Extracted:

- Local SAM hashes
- Cached domain credentials
- LSA secrets

---

### 5. Hash Cracking

Recovered additional local administrator password:

```
[REDACTED_PASSWORD]
```

---

### 6. Password Reuse Discovery

Observed password reuse at the host level:

- Local administrator accounts shared identical hashes within the same machine
- Different machines used weak but slightly varied passwords

---

### 7. Pass-the-Hash

Used NTLM hashes to authenticate without knowing plaintext passwords.

---

### 8. Lateral Movement

Successfully accessed multiple machines due to weak credential hygiene and password reuse.

---

## 🔍 Key Findings

- Credential exposure via LLMNR poisoning
- Weak password patterns across systems
- Local administrator password reuse per host
- Successful Pass-the-Hash authentication
- Lateral movement achieved without plaintext credentials

---

## 🛡️ Defensive Recommendations

- Disable LLMNR and NBT-NS
- Enforce strong and unique passwords
- Avoid local administrator password reuse
- Enable SMB signing
- Monitor credential dumping tools and unusual authentication attempts

---

## 🧠 Conclusion

This lab highlights how weak configurations and poor password practices can lead to full network compromise. Starting from a single captured hash, an attacker can escalate access and move laterally across systems.

---
