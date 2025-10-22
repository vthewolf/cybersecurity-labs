# Lab Documentation: Cracking SSH Key Passwords

This lab demonstrates how to crack the passphrase protecting an **SSH private key (`id_rsa`)** using the `ssh2john.py` utility and John The Ripper (JtR).

## 1. Environment and Hash Preparation

Since the `ssh2john` command was not found, the Python version (`ssh2john.py`) located in `/opt/john/` was executed. The private key (`id_rsa`) was converted into a hash format, and the output was redirected (`>`) to `id_rsa_hash.txt`.

**Commands:**

```bash
ls
ssh2john
python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
ls
```
Terminal Output Snippet:
```
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task11$ ls
id_rsa
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task11$ ssh2john
ssh2john: command not found
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task11$ python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task11$ ls
id_rsa id_rsa_hash.txt
```

## 2. Cracking the Hash with John The Ripper
The generated hash file (id_rsa_hash.txt) was processed by John The Ripper using a dictionary attack against the rockyou.txt wordlist.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
```
Cracked Passphrase Output:

John successfully cracked the hash, revealing the passphrase: `mango`.

```user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task11$ john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (SSH, SSH private key [RSA/DSA/EC/OPENSSH 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=8crypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 2 OpenMP threads
Note: Passwords longer than 10 [worst case UTF-8] to 32 [ASCII] rejected
Press 'q' or Ctrl-C to abort, 'h' for help, almost any other key for status
**mango** (id_rsa)
1g 0:00:00:00 DONE (2025-10-22 14:07) 50.00g/s 214400p/s 214400c/s 214400C/s praise..mango
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task11$
```
The passphrase for the id_rsa private key is `mango`.

## 4. Evidence
!(Capture)[./image.png]
