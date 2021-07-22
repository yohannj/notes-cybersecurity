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

# Discuss with Netcat
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