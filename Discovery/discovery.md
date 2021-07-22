# Unix commands
## Listing open hosts
```bash
# Send ICMP (ping) to each possible IP except TCP SYN to port 443 and TCP ACK to port 80
# Port scanning is deactivated
sudo nmap -sn RANGE # nmap -sn 192.168.0.1-254
sudo nmap -sn CIDR  # nmap -sn 192.168.0.0/24
```
## Listing open ports
```bash
# nmap contact every ports of the TARGET_IP

# -sS = TCP SYN scan
# That way we check if ports are available, and send back a RST packet. Old Intrusion Detection systems and logging systems don't care about these connections.
# HOWEVER unstable services may be brought DOWN by SYN scan
sudo nmap -sS -A -p- TARGET_IP

# -sT = TCP Connect scan
sudo nmap -sT -A TARGET_IP

# -sN = TCP Null scan
# Remove all flags from TCP request. Per RFC we should receive a RST response if the port is closed
# Aim is to bypass some firewall rules.
# Some target may send RST whether the port is closed or NOT. Some Microsoft Windows or Cisco are in this range of target.
sudo nmap -sN -A TARGET_IP

# -sF = TCP FIN scan
# Similar to -sN in behaviour, though the FIN flag is sent this time. This flag usually serves to gracefully close an active connection
sudo nmap -sF -A TARGET_IP

# -sX = TCP Xmas scan
# Similar to -sN in behaviour, though 3 flag are sent to form a malformed TCP packet.
sudo nmap -sX -A TARGET_IP

# -sU = UDP scan
# Most of the time no response from the server, consider the port to be open/filtered. Should receive a ICMP (ping) if the port is closed.
# It is SLOW, because we "wait" hoping for a response. To make up for it, we can use `--top-ports 20` to only scan the top 20 most common ports.
sudo nmap -sU --top-ports 20 TARGET_IP

# -pN = consider the host alive without sending ICMP (ping)
# It increases the scanning time significantly, but can bypass some firewall
# For more flag to bypass a firewall: https://nmap.org/book/man-bypass-firewalls-ids.html
sudo nmap -sT -Pn TARGET_IP

# -A = OS detection + version detection + script scanning + traceroute
sudo nmap -sU -A TARGET_IP

# -O = OS detection
sudo nmap -sU -O TARGET_IP

# -sV = Try to determine service behind a port + its version
sudo nmap -sU -sV TARGET_IP

# -v = verbose
sudo nmap -sU -v TARGET_IP

# -vv = even more verbose, we can add even more v if needed
sudo nmap -sU -vv TARGET_IP

# -oA = Store results in normal, XML and grepable format
sudo nmap -sU -oA OUTPUT_FILE_PREFIX TARGET_IP

# -oN = Store results in normal format
sudo nmap -sU -oN OUTPUT_FILE TARGET_IP

# -p 80 = only scan port 80
sudo nmap -sU -p 80 TARGET_IP

# -p 1000-1500 = only scan ports ranging from 1000 to 1500 included
sudo nmap -sU -p 1000-1500 TARGET_IP

# -p- = scan all ports
sudo nmap -sU -p- TARGET_IP

# --script=CATEGORY = Activate all scripts in the CATEGORY category (e.g. vuln)
# Actually CATEGORY can even be a single or multiple specific scripts.
#
# Scripts arguments should be provided using `--script-args SCRIPT_NAME.ARGUMENT` e.g. `--script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'`
#
# To get HELP on a script, call `nmap --script-help SCRIPT_NAME`
#
# Script can be searched on https://nmap.org/nsedoc/
# Or locally in folder /usr/share/nmap/scripts and plain text file: /usr/share/nmap/scripts/script.db
#
# Scripts can be updated through `sudo apt update && sudo apt install nmap`
# They can also be downloaded and installed: `sudo wget -O /usr/share/nmap/scripts/SCRIPT_NAME.nse https://svn.nmap.org/nmap/scripts/SCRIPT_NAME.nse && nmap --script-updatedb`
sudo nmap -sU --script=CATEGORY TARGET_IP # sudo nmap -sU --script=vuln 172.0.0.1
```

## Check access to server
```bash
# Check the target is accessible + retrieve its IP (over ICMP)
ping TARGET_URL_OR_IP

# Same as ping, but sends packet every 500ms
ping -i 0.5 TARGET_URL_OR_IP

# Similar to ping, including information on all intermediate servers the request went through (over UDP)
traceroute TARGET_URL_OR_IP

# Same as traceroute, but over ICMP (if UDP is filtered)
sudo traceroute -I TARGET_URL_OR_IP

# Same as traceroute, but over TCP (if UDP is filtered)
sudo traceroute -T TARGET_URL_OR_IP
```

## General information
```bash
# OS info
cat /etc/os-release

# List users
## Find min/max UID of normal users
grep -E '^UID_MIN|^UID_MAX' /etc/login.defs
## Compare values with what is in
cat /etc/passwd

# Check content available
## Look for any file under FOLDER with the type TYPE
## TYPE values: d = directory; f = regular file; l = symlink; s = socket
## use `man` for other weird possibilities
find FOLDER -type TYPE

find FOLDER -user USERNAME -group GROUPNAME
find FOLDER -uid USERID -gid GROUPID
```

## Domain info
```bash
# Registered info about a domain
whois TARGET_URL_OR_IP

# Ask domain info to some recursive DNS servers
dig TARGET_URL @DNS_SERVER_IP # dig google.com @1.1.1.1
```

## SMTP discovery
```bash
# Not available at OSCP
# Get fun with msfconsole
```

## Website
```bash
# GET request
curl TARGET_IP

# Choose TYPE of request
curl -X TYPE TARGET_IP # curl -X POST 127.0.0.1

# Send DATA
curl -X POST --data DATA TARGET_IP

# Store cookies
curl -b PATH_TO_STORE_COOKIES TARGET_IP

# Set cookies
curl -c PATH_TO_STORED_COOKIES TARGET_IP
curl -c 'KEY1=VAL1;KEY2=VAL2' TARGET_IP
```

# Windows commands
## Check access to server
```bash
# Check the target is accessible + retrieve its IP (over ICMP)
ping TARGET_URL_OR_IP

# Same as ping, but sends packet every 500ms
ping -i 0.5 TARGET_URL_OR_IP

# Similar to ping, including information on all intermediate servers the request went through (over ICMD)
tracert TARGET_URL_OR_IP
```

## Listing open ports
Use nmap. Refer to Listing open ports from the linux commands.