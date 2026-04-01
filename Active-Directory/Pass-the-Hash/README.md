# 🛡️ Pass-the-Hash / Pass-the-Password – Mitigation

## 📌 Overview

Pass-the-Hash (PtH) and Pass-the-Password attacks allow attackers to authenticate to systems using stolen credentials (hashes or plaintext passwords) without knowing the original password.

These attacks are common in Active Directory environments, especially when weak security practices are in place.

---

## 🎯 Objective

Understand how to reduce the risk of Pass-the-Hash and Pass-the-Password attacks by applying proper security controls.

---

## 🔐 Mitigation Techniques

### 1. Limit Account Re-use

- Avoid re-using local administrator passwords across multiple systems  
- Disable default accounts such as **Guest** and unused **Administrator** accounts  
- Apply **Least Privilege Principle** (only required users should have admin access)  

👉 **Why it matters:**  
If the same password is used across systems, compromising one machine can lead to full network compromise.

---

### 2. Use Strong Passwords

- Use passwords longer than **14 characters**  
- Avoid common words and predictable patterns  
- Prefer **passphrases** (long, easy-to-remember sentences)  

👉 **Example:**  
❌ `Password123`  
✅ `MySecureLifeInBarcelona2024!`

👉 **Why it matters:**  
Stronger passwords create stronger hashes, making them harder to crack or reuse.

---

### 3. Privilege Access Management (PAM)

- Use systems that provide **temporary privileged access**  
- Automatically **rotate passwords** after use  
- Monitor and control access to sensitive accounts  

👉 **Why it matters:**  
Even if an attacker captures a hash, it becomes useless after password rotation.

---

## 🌍 Real World Scenario

In many environments, all systems share the same local administrator password.

An attacker compromises one machine, extracts the hash, and uses Pass-the-Hash to move laterally across the network — gaining access to multiple systems without cracking any password.

---

## 🧠 Key Insight

Pass-the-Hash attacks are most effective when:

- Passwords are reused  
- Too many users have admin privileges  
- Passwords are not rotated regularly  

---

## 🛡️ Defense Summary

- Use unique passwords for each system  
- Enforce strong password policies  
- Apply least privilege access  
- Implement Privileged Access Management (PAM)  
- Regularly rotate credentials  

---

## ⚠️ Notes

- Avoid exposing real credentials or internal IPs in documentation  
- Always follow ethical hacking guidelines and proper authorization  

---

## 📚 Related Topics

- SMB Relay Attack  
- Lateral Movement Techniques  
- Active Directory Security  
- Credential Dumping  
