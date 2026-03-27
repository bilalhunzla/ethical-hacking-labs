# 🧠 PlumHound – Quick Notes (PEH)

## 📌 Purpose

PlumHound is a reporting and analysis tool for Active Directory environments.

It works on BloodHound data stored in Neo4j and generates readable security insights.

---

## 🔗 Relationship Between Tools

- bloodhound-python → collects AD data
- Neo4j → stores data
- BloodHound → visualizes relationships
- PlumHound → generates reports from data

---

## ❗ Important Concept

PlumHound does NOT perform enumeration itself.

It only queries existing data from the Neo4j (BloodHound) database.

---

## ⚠️ Kali Linux Issue

Error:
externally-managed-environment

Cause:
Kali blocks system-wide pip installs (PEP 668)

---

## ✅ Fix (Best Practice)

Use virtual environment:

```bash
cd ~/PlumHound
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

```

## Run PlumHound

python3 PlumHound.py --easy -p neo4j1

## 📊 Output

Domain Users
Service Accounts
AD objects
Relationships

## 🧠 Key Learning Points

Works only if BloodHound data exists
Does not require target machines to be ON
Used for reporting, not exploitation
Depends on data quality

## 🔍 Usage Context

Red Team
Identify attack paths
Privilege escalation opportunities
Blue Team
Understand exposure
Improve security posture

## 🧩 Pro Insight

"PlumHound is only as powerful as the data you feed into BloodHound."
