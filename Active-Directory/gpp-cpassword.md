# GPP cPassword Attack (Quick Note)

## What is it?

Group Policy Preferences stored passwords in encrypted form (cPassword)

## Issue

Encryption key is public → anyone can decrypt

## Steps

1. Access SYSVOL share
2. Find XML files (Groups.xml etc.)
3. Extract cPassword
4. Decrypt using:
   gpp-decrypt <value>

## Impact

Low privilege user → plaintext credentials

## Note

Still relevant in old environments
