# Lab Documentation: Cracking Password-Protected ZIP Files

This lab demonstrates the process of cracking a password-protected ZIP archive using the `zip2john` utility and the John The Ripper (JtR) password cracker. The goal was to retrieve the content of the `flag.txt` file inside `secure.zip`.

## 1. Environment and File Preparation

The first step involved navigating to the correct directory and using the `zip2john` utility to convert the protected `secure.zip` file into a hash format readable by John The Ripper. The output was redirected (`>`) to a file named `zip_hash.txt`.

**Commands:**

```bash
cd John-the-Ripper-The-Basics/Task09
zip2john secure.zip > zip_hash.txt
cat zip_hash.txt
```
Terminal Output Snippet:
```
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task09$ zip2john secure.zip > zip_hash.txt
Ver 1.0 efh 5455 efh 7875 secure.zip/zippy/flag.txt PKZIP Encr: 2b chk, TS_chk, complen=38, decmplen=26, crc=849AB5A6 ts=b689 cs=b689 type=0
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task09$ cat zip_hash.txt
secure.zip/zippy/flag.txt:$pkzip$1*2*2*0*26*1a*849ab5a6*0*48*0*26*b689*964fa5a31f8cefe8e6b3456b578d66a08489def78128450ccf07c28dfa6c197fd148f696e3a2*$*pkzip:zippy/flag.txt:secure.zip::secure.zip
```
1. Cracking the Hash with John The Ripper
The generated hash file (zip_hash.txt) was fed into John The Ripper, utilizing the common rockyou.txt wordlist for a dictionary attack.

Command:

```Bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```
Cracked Password Output:

John successfully cracked the hash, revealing the password: pass123.
```
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task09$ john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 2 OpenMP threads
Note: Passwords longer than 21 (worst case UTF-8) to 63 [ASCII] rejected
Press 'q' or Ctrl-C to abort, 'h' for help, almost any other key for status
**pass123** (secure.zip/zippy/flag.txt)
1g 0:00:00:00 DONE (2025-10-22 13:26) 50.00g/s 409600p/s 409600c/s 409600C/s newzealand..total90
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
user@ip-10-10-81-237:~/John-the-Ripper-The-Basics/Task09$ 
```
2. Extracting the Flag File
With the password (pass123) confirmed, the final step was to use the unzip utility to extract the contents of the archive using the password flag (-P).

Extraction and Flag Retrieval Commands:
```
Bash

unzip -P pass123 secure.zip
cat flag.txt
The file flag.txt was successfully extracted, completing the laboratory exercise.
```
