File Transfer Protocol uses a client-server model to transfer files, relays commands and data.
https://www.ietf.org/rfc/rfc959.txt

Default port: 21

Up to two types of connexions are supported, Active and Passive.
* Active: client opens a port and listens. The server will connect to it.
* Passive: servers opens a port and listens. The client will connect to it.

```bash
# Open ftp client locally
ftp

# Connection to an ftp server
ftp TARGET_IP # When prompt for account, try Anonymous
```