# Misc tools
## MSConfig
Help diagnose startup issues (https://docs.microsoft.com/en-us/troubleshoot/windows-client/performance/system-configuration-utility-troubleshoot-configuration-errors)

The tools tab is useful to see the different tool proposed by the system and a short description of each of them.

## Command line manual pages
Use `/?` after a command name

# Task Manager
taskmgr

# Computer Management
## Task Scheduler
This is a tool that allows predefined actions to be automatically executed whenever a certain set of conditions is met
Another way to set up tasks is through: `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run`

## Event Viewer
The Event Viewer logs events that happen across the device.
The reason Event Viewer is important is because it can be used to forward the events to a SIEM (Security Information and Event Manager) which helps the IT team of a company determine possible malicious activities.

| event type         | location                | EventId |
| ------------------ | ----------------------- | ------- |
| Logon              | Windows Logs > Security | 4624    |
| Logoff             | Windows Logs > Security | 4634    |
| Special priviledge | Windows Logs > Security | 4672    |

## Shared Folders
Directory or Folder that can be shared across the network and can be accessed by multiple users.

## Local users & computers
Using local users and computers we can create users, add them to different built-in groups, and they can be given different levels of access.

## Performance Monitor
Performance Monitor monitors the different activities across the device such as CPU usage, memory usage, etc.

## Disk Management
Using Disk Management you can shrink, expand, create new partitions (drives) and format the partitions.

## Services & Applications
It is possible to check the running services on the system and you have the ability to start, stop or restart them.

# Update and security tools
## Windows Update
Serves to update windows.
Common patches are done on "Patch Tuesday", every 2nd Tuesday of the month.

## Windows Security
Tools to protect the device and its data.
Acts at network and application level.

### Virus & threat protection
See current threats and history, including action applied and quarantined files.
Possibility to scan on demand.

Settings to activate/deactivate protections can also be found here.

### Firewall & network protection
Defines three profiles, domain, private and public network. Settings of these profiles will be used by Windows firewall when connected to internet.

### App & browser control
Microsoft Defender SmartScreen protects against phishing or malware websites and applications, and the downloading of potentially malicious files.

### Device security
Additional protection (off by default) regarding misusage of low-level drivers.

## BitLocker
Encrypt data on disk.

## Volume Shadow Copy Service
Backup of the data. Must be saved on an external device to avoid an attacker to delete them.

# Local Security Policy
Group of settings that can be configured to strengthen the computer's security.
Even though most policy settings in Windows are fine, there are a few that need adjusting for enhanced security. (min password length, password complexity level, disable guest & local administrator accounts, ...)

# Disk Cleanup
Can be used to delete files that are no longer needed by the system and are just adding up to the computer disk space.
Running Disk Cleanup as administrator we can also clean system files.

# Registry Editor
Contains system settings and a lot of information from hardware to software.
Can be seen as a K/V store.

## Registry Editor (Regedit)
HKEY_CLASSES_ROOT
HKEY_CURRENT_USER
HKEY_LOCAL_MACHINE
HKEY_USERS
HKEY_CURRENT_CONFIG

Registries can be browsed within Powershell.
```PowerShell
cd HKLM:\
cd HKCU:\
```

Registries can also be edited within Powershell.
```PowerShell
reg /?
```

# Command-line tools
## CMD
Provide MS-DOS capabilities in CLI.

## Powershell
Advanced administration capabilities compared to CMD.
Can also be used to execute PowerShell scripts.

## Windows Terminal
Available in Microsoft Store, replaces both Powershell and CMD and provides additional UX features (e.g. multiple tab).