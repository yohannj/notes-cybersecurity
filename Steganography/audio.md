# Cut file
```python
f = open('transmission.wav', 'rb').read()
f = f.split(b'\x00' * 30000)[1:]
out = ""
for x in f:
    y = x.split(b'\x00' * 5200)[1:][:5]
    L = ([0 if len([z for z in y_ if z != 0]) > 15000 else 1 for y_ in y])
    if L[4] == 1:
        out += " "
    else:
        out += str(L[0] ^ 1)
print(out)
```