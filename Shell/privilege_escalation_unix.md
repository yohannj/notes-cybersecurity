# Use linpeas (linus priv esc awesome script)
```bash
# Prepare receiver, expecting a file on port 1234
nc -l -p 1234 > /tmp/linpeas.sh
```
```bash
# Send the file to TARGET
nc -w 3 TARGET 1234 < Scripts/privilege-escalation-awesome-scripts-suite/linPEAS/linpeas.sh
```

# Use winpeas (windows priv esc awesome script)
Find a way to have Scripts/privilege-escalation-awesome-scripts-suite/winPEAS/winpeas.bat
