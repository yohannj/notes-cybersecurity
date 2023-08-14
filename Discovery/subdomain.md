# Check SSL/TLS history
https://crt.sh/

# Search engine
## Automated (not a great coverage)
```bash
python2.7 /home/vagrant/Scripts/Sublist3r/sublist3r.py -d DOMAIN_NAME
```
## Google
`-site:www.SITENAME.com  site:*.SITENAME.com`

# dns bruteforce
```bash
dnsrecon -d DOMAIN_NAME [-D WORDLIST] -t brt
```

# Fuzzing on host header
```bash
wfuzz --hh 2395 -z file,/usr/share/dnsrecon/namelist.txt -H "Host: FUZZ.DOMAIN_NAME" -u http://TARGET_IP

wfuzz -c -f subdomains_res.txt --hh 85 -Z -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.TARGET" http://TARGET 
```
