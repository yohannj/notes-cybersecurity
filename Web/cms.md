# Wordpress

```bash
#Brute force found users and search for vulnerabilities using a free API token (up 50 searchs)
wpscan --rua -e ap,at,tt,cb,dbe,u,m --url http://TARGET [--plugins-detection aggressive] --api-token <API_TOKEN> --passwords /usr/share/wordlists/external/SecLists/Passwords/probable-v2-top1575.txt
```