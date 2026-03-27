# 📝 PingCastle – Quick Notes (Active Directory Enumeration)

## 📌 What is PingCastle?

PingCastle is a tool used to **analyze Active Directory security** and find misconfigurations, weak policies, and risks.

---

## 🎯 Purpose

- Identify security weaknesses in AD
- Detect misconfigured users/groups
- Analyze domain policies
- Generate a risk score

---

## ⚙️ Where to Run?

- Run on **domain-joined machine** ✅
- Example: THEPUNISHER-2
- Do NOT run on Kali ❌

---

## 🚀 Basic Execution

```bash
PingCastle.exe
```

Steps:

1. Select → Healthcheck (default)
2. Privileged Mode → Yes (1)
3. Domain → Press Enter (default)

---

## 📄 Output

```bash
ad_hc_<domain>.html
```

Example:

```bash
ad_hc_MARVEL.local.html
```

---

## 🔍 What PingCastle Checks?

- Users & Groups
- Password policies
- Privileged accounts
- Trust relationships
- Domain configurations
- Security misconfigurations

---

## ⚠️ Important Concepts

### 🔴 Risk Score

- Shows overall security level of domain
- Higher score = more risk

---

### 🔴 Privileged Mode

- Deep scan
- More accurate results
- Recommended for labs

---

## 🧠 Common Findings

- Weak password policy
- Too many privileged users
- SMB signing disabled
- Old protocols enabled
- Misconfigured permissions

---

## 🛠️ Real-World Use

- Active Directory auditing
- Internal penetration testing
- Blue team security checks
- Risk assessment reports

---

## 📌 Exam Tips

- Always run **healthcheck**
- Use **privileged mode**
- Understand **risk score**
- Focus on **high-risk findings**

---

## 💡 Pro Tip

PingCastle is a **quick overview tool**, not exploitation tool.

👉 Use it to:

- Find weaknesses
- Then use other tools (BloodHound, CrackMapExec, etc.)

---

## 🔗 Related Tools

- BloodHound (attack path analysis)
- CrackMapExec (post-exploitation)
- Impacket (lateral movement)
