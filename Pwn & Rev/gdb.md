# Launch program with gdb
```bash
gdb PROGRAM_NAME
```

# Read function
```gdb
disas FUNCTION_NAME
```

# Break at a specific addr
```gdb
b* 0x00000000004013f7
```

# Get pointer addr
```gdb
p &str
```

# Read 64bits variable
```gdb
# Read as HEX
x/gx VARIABLE_ADDR

# Read as STR
x/xs VARIABLE_ADDR
```
