# Variables
p - prime number
q - prime number
m - message
n - `p * q`
e - with n, construct public key
d - with n, construct private key
c - cyphertext

# Reading a character
A message is a list of numbers.
For each of them, pow(number, d, n) and take their chr()
```python
print(''.join([chr((block ** d) % n) for block in blocks]))
```

# Tools
https://github.com/Ganapati/RsaCtfTool
https://github.com/ius/rsatool