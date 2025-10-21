# Cracking Windows Authentication Hashes (NTLM)

## General concept
- **Authentication hashes** are the hashed versions of passwords stored by operating systems.  
  To obtain them in real scenarios you typically need privileged access on the target machine (elevated user).

## NT Hash / NTLM
- **NT hash** (also referred to as **NTLM**) is the format modern Windows systems use to store user and service passwords.  
- Passwords are not stored in plaintext but as hashes (NT hash / NTLM) inside the account database.

## Where to find Windows hashes
- **SAM (Security Account Manager):** local file that stores account info and hashes on individual Windows machines.  
- **NTDS.dit:** Active Directory database that contains domain account hashes.  
- Tools like **Mimikatz** can extract these hashes if you already have privileged access.

## Alternative to cracking: Pass-the-Hash
- Sometimes you don’t need to crack the hash: with **pass-the-hash** you can reuse the hash directly to authenticate laterally (if the environment accepts it), avoiding the need to recover the plaintext password.  
- However, if password policies are weak, cracking the hash can reveal the actual password and enable additional misuse (password reuse, lateral moves, etc.).

## Lab practice
- Apply the techniques learned (identify hash format, use wordlists / John the Ripper) to try cracking the `ntlm.txt` file.  
- Lab path on the VM:


## Key point for the lab
- **You need context and privileges** to obtain Windows hashes in real-world scenarios. In the lab you will practice cracking once you have the hash and learn when **pass-the-hash** is more useful than cracking the password.
