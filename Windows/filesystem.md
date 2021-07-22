# Important folders
## PerfLogs
Stores the system issues and other reports regarding performance

## Program Files and Program Files (x86)
Default location for programs

## Users
Store the users on the filesystem. It also stores users generated data (Ex: Saving a file on your Desktop)

## Windows
Contains the code to run the operating system and some utility tools

### Password location
C:\Windows\System32\config\SAM

# Permissions
Permissions are granted to a user/users/a group/groups.
Permissions can be check using `icacls`

## Different kind of permissions
### Full control
Allow/Deny setting the ownership of the folder, set permission for others, modify, read, write, and execute files.

### Modify
Allow/Deny modifying, read, write, and execute files.

### Read & execute
Allow/Deny reading and execute files.

### List folder contents
Allow/Deny listing the contents (files, subfolders, etc) of a folder.

### Read
Allow/Deny reading files.

### Write
Allow/Deny writing data to the specified folder (automatically set when "Modify" right is checked).

## icacls
### Checking permissions
```PowerShell
icacls C:\Users

# C:\Users AUTORITE NT\Système:(OI)(CI)(F)
#          BUILTIN\Administrateurs:(OI)(CI)(F)
#          BUILTIN\Utilisateurs:(RX)
#          BUILTIN\Utilisateurs:(OI)(CI)(IO)(GR,GE)
#          Tout le monde:(RX)
#          Tout le monde:(OI)(CI)(IO)(GR,GE)
```

I - permission inherited from the parent container
F - full access (full control)
M - Modify right/access
OI - object inherit
IO - inherit only
CI - container inherit
RX - read and execute
AD - append data (add subdirectories)
WD - write data and add files

### Setting permissions
```PowerShell
icacls tmp /setowner xxx@xxx.xxx
# processed file: tmp
# Successfully processed 1 files; Failed processing 0 files
```
