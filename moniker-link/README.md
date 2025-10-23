1. From the attacking machine, we create a script with the contents of the file in the `exploit.py` repository.

2. We run it. If we don't have permissions, we give them with `chmod +x exploit.py`

3. We modify the script data with the IP addresses of the attacker and the person who will receive the email.

4. Run `responder -I ens5` to start listening for responses.

5. Wait for the recipient to click on the malicious link.
