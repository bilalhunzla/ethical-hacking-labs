# Troubleshooting Notes

Common issues faced during Active Directory labs and their fixes.

## Issue 1: MD4 Hash Error

### Problem

Error while running ldapdomaindump related to MD4 hashing.

### Cause

Python/OpenSSL compatibility issue.

### Fix

```bash
python3 -c "import hashlib; print(hashlib.new('md4'))"

```

## Issue 2: Tool Version Mismatch

### Problem

Commands from older labs not working.

### Cause

Check official documentation
Update tool:

### Fix

```bash
pip install impacket --upgrade
```

## Lesson Learned

Always verify tool versions and adapt commands accordingly.
gvctf
