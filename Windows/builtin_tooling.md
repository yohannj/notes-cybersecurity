# Computer Management
## Task Scheduler
This is a tool that allows predefined actions to be automatically executed whenever a certain set of conditions is met

## Event Viewer
The Event Viewer logs events that happen across the device.
The reason Event Viewer is important is because it can be used to forward the events to a SIEM (Security Information and Event Manager) which helps the IT team of a company determine possible malicious activities.

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