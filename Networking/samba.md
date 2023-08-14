# Introduction
"Server Message Block" is a protocol to share files, printers, serial ports and other resources.
Based on TCP/IP


```bash
# Get userlist, machine list, namelist dump, sharelist, password policy info, group and member list
enum4linux -a TARGET_IP

# ls -l / --> Try guest as default USERNAME
smbmap -H TARGET_IP -u USERNAME

# ls -l /FOLDER_NAME
smbmap -H TARGET_IP -u USERNAME -r FOLDER_NAME

# Download /PATH_TO_FILE from target to local
smbmap -H TARGET_IP -u USERNAME --download PATH_TO_FILE

# Upload /PATH_TO_FILE from target to local
smbmap -H TARGET_IP -u USERNAME --upload PATH_TO_FILE

# List shares
smbclient -L //TARGET_IP -U USER -p PORT

# Connect to a share
smbclient //TARGET_IP/FOLDER_NAME -U USER -p PORT
```
