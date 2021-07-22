# Web Server
## Dirsearch
https://github.com/maurosoria/dirsearch

```bash
python3 /home/vagrant/Scripts/dirsearch/dirsearch.py -u http://TARGET -e php --exclude-status 403,401
```

## Fuzz
https://wfuzz.readthedocs.io/en/latest/user/basicusage.html

```bash
# Looking for a directory
wfuzz -w wordlist/general/common.txt http://TARGET/FUZZ
wfuzz -w /usr/share/wordlists/SecLists/Discovery/Web-Content/dirsearch.txt http://TARGET/FUZZ

# Looking for a file
wfuzz -w wordlist/general/common.txt http://TARGET/FUZZ.php

# Replace a specific query params
wfuzz -z range,0-10 --hl 97 http://testphp.vulnweb.com/listproducts.php?cat=FUZZ

# Replace parameters in the body of a POST request
wfuzz -z file,/usr/share/wordlists/wfuzz/others/common_pass.txt -d "uname=admin&pass=FUZZ" http://TARGET

# Replace JSON parameters in the body of a POST request
wfuzz -H "Content-Type: application/json" -z file,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/best1050.txt -d '{"email":"EMAIL_ADRESS","password":"FUZZ"}' http://TARGET
```

# Password
## Identify hash algorithm
```bash
# -m Prints hashcat mode
hashid -m 'HASH_TO_IDENTIFY'
```

## Crack
```bash
# See `man` for the appropriate MODE = encryption method
# hashcat is also available on Windows to use with the GPU (x10 perf), along with crackstation.lst for a huge dictionary
hashcat -m MODE -a 0 PATH_TO_PASSWORDS PATH_TO_DICTIONARY
```

```powershell
# See `--help` for the appropriate MODE = encryption method
hashcat.exe -m MODE -a 0 PATH_TO_PASSWORDS PATH_TO_DICTIONARY
hashcat.exe -m 3200 -a 0 ../hashed_password.txt  ../rockyou.txx
```

## Generate masks for hashcat (and others)
Using `-a 3`, hashcat will take a list of masks to generate passwords to use against the hash. => https://hashcat.net/wiki/doku.php?id=mask_attack
We can write those by hand, or use mask processor to create that for us.

### Masks
Masks are created using charsets and hardcoded characters

#### Built-in charsets
| charset | matches                           |
| ------- | --------------------------------- |
| ?l      | lowercase letters                 |
| ?u      | uppercase letters                 |
| ?d      | 0123456789                        |
| ?h      | 0123456789abcdef                  |
| ?H      | 0123456789ABCDEF                  |
| ?s      |  !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~ |
| ?a      | ?l?u?d?s                          |
| ?b      | 0x00 - 0xff                       |

#### Custom charsets
Up to 4 custom charsets can be created, using options `-1 CHARSET`, `-2 CHARSET`, `-3 CHARSET`, `-4 CHARSET`.
For example, to match 5 lowercase or digits:
```powershell
hashcat.exe -m MODE -a 3 -1 ?l?d ?1?1?1?1?1
```

```bash
#mp = mask processor
mp64 -o bla.rule '^?l $?d‘
```

# Zip / RAR / SSH password
```bash
# First, extract/reformat in a way that john can handle
zip2john PATH_TO_ZIP > hash.txt
rar2john PATH_TO_RAR > hash.txt
python /usr/share/john/ssh2john.py PATH_TO_ID_RSA > hash.txt

# Then use john to bruteforce the password
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

# Database
```bash
medusa -h TARGET_IP -U /usr/share/wordlists/SecLists/Usernames/mssql-usernames-nansh0u-guardicore.txt -P M3g4c0rp123 -O medusaOutput.txt -M mssql
```

# FTP
```bash
# -t 16 = 16 concurrent requests
# -P path to dictionary
# -vV very verbose
hydra -t 16 -l USER -P /usr/share/wordlists/rockyou.txt -vV TARGET_IP PROTOCOL
```

# SMTP
Cf hydra in #FTP