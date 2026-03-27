# PlumHound Installation & Enumeration (Kali Linux)

## 📌 Overview

This lab demonstrates how to install and run PlumHound on modern Kali Linux, solve pip installation errors, and generate reports using BloodHound data.

---

## ❌ Problem Encountered

While installing dependencies:

```bash
sudo pip3 install -r requirements.txt
```

Error:

externally-managed-environment

## Cause

Modern Kali Linux blocks system-wide pip installations (PEP 668) to protect system packages.

## ✅ Solution (Best Practice)

1. Copy tool to home directory
   cp -r /opt/PlumHound ~/PlumHound

2. Create virtual environment
   cd ~/PlumHound
   python3 -m venv venv

3. Activate environment
   source venv/bin/activate

4. Install dependencies
   pip install --upgrade pip
   pip install -r requirements.txt

## Running PlumHound

```bash
python3 PlumHound.py --easy -p <neo4j_password>
```

## Result

PlumHound successfully connected to Neo4j and retrieved Active Directory data such as:

Domain Users
Service Accounts
Default Accounts

## Key Learning

PlumHound does NOT collect data itself
It uses the BloodHound (Neo4j) database
Lab machines are not required once data is stored

## Tools Used

bloodhound-python (data collection)
Neo4j (database)
BloodHound (visualization)
PlumHound (reporting)
