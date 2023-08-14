# Linux
Look for a .ssh of a user (retrieve the key to log in, add myself in their authorized_keys)

Check if any if writable: /etc/shadow or /etc/passwd
or check https://github.com/dirtycow/dirtycow.github.io/wiki/PoCs

# Windows
Look for creds.
Maybe C:\Program Files\FileZilla Server\FileZilla Server.xml or C:\xampp\FileZilla Server\FileZilla Server.xml

Create your own user:
```powershell
net user USERNAME PASSWORD /add
net localgroup administrators USERNAME /add
```