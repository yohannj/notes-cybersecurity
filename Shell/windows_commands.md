# cmd
## List directory content
```bash
dir PATH_TO_DIRECTORY #(dir C:\)
```

## Read content of a file
```bash
type PATH_TO_FILE
```

## Launch powershell
```bash
powershell
```

# powershell
## Bunch of commands
https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993

## Download file
```bash
wget URL -OutFile out.html
wget HOST:IP/PATH_TO_FILE -OutFile out.html
```

```bash
# list all operating systems on the domain
Get-NetComputer -fulldata | select operatingsystem

# list all users on the domain
Get-NetUser | select cn

# list all groups on the domain
Get-NetGroup
```
