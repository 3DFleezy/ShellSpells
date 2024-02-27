# Shares

## <mark style="color:red;">Enumerate</mark>

| Command                                                        | Description                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------------- |
| <mark style="color:yellow;">`net share`</mark>                 | Lists or creates shares on the local computer.                 |
| <mark style="color:yellow;">`net use`</mark>                   | Displays connected network shares.                             |
| <mark style="color:yellow;">`net share`</mark>                 | Lists all shared resources on the local computer.              |
| <mark style="color:yellow;">`Get-SmbShare`</mark>              | PowerShell cmdlet to list SMB shares.                          |
| <mark style="color:yellow;">`fsmgmt.msc`</mark>                | Opens the Shared Folders Management Console (GUI).             |
| <mark style="color:yellow;">`Get-WmiObject Win32_Share`</mark> | Retrieves shared resources using WMI in PowerShell.            |
| <mark style="color:yellow;">`Get-SmbShareAccess`</mark>        | Retrieves access permissions for an SMB share in PowerShell.   |
| <mark style="color:yellow;">`net session`</mark>               | Lists or disconnects sessions between the computer and others. |
| <mark style="color:yellow;">`net file`</mark>                  | Lists or closes open files shared on the computer.             |

## <mark style="color:red;">Create/Connect</mark>

| Command                                                                      | Description                                                    |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------- |
| <mark style="color:yellow;">`net share [NetShareName]=[Drive\\Share]`</mark> | Create a network share                                         |
| <mark style="color:yellow;">`net share <sharename>=<drive>:<path>`</mark>    | Map share from remote host                                     |
| <mark style="color:yellow;">`net share <sharename> /delete`</mark>           | Delete network share                                           |
| <mark style="color:yellow;">`net share progfiles="C:\\Program Files"`</mark> | Share Program Files directly as progfiles                      |
| <mark style="color:yellow;">`net use`</mark>                                 | Connects, disconnects, and lists network connections.          |
| <mark style="color:yellow;">`net use Z:\\10.50.50.52\classrom`</mark>        | Connect to a share                                             |
| <mark style="color:yellow;">`New-SmbShare`</mark>                            | Creates a new SMB share in PowerShell.                         |
| <mark style="color:yellow;">`Remove-SmbShare`</mark>                         | Removes an SMB share in PowerShell.                            |
| <mark style="color:yellow;">`Set-SmbShare`</mark>                            | Modifies settings of an SMB share in PowerShell.               |
| <mark style="color:yellow;">`Grant-SmbShareAccess`</mark>                    | Grants access permissions to an SMB share in PowerShell.       |
| <mark style="color:yellow;">`Revoke-SmbShareAccess`</mark>                   | Revokes access permissions from an SMB share in PowerShell.    |
| <mark style="color:yellow;">`net session`</mark>                             | Lists or disconnects sessions between the computer and others. |
| <mark style="color:yellow;">`net session /list`</mark>                       | Lists shares                                                   |
| <mark style="color:yellow;">`net session \\ComputerName /delete`</mark>      | Deletes connections remotely                                   |
| <mark style="color:yellow;">`net file`</mark>                                | Lists open files shared on the computer. Shows File IDs.       |
| <mark style="color:yellow;">`net file <FileID> /close`</mark>                | Close the specified file that is open on the network.          |

## <mark style="color:red;">Registry Locations</mark>

SMB Shares:

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Shares</mark>

This key contains information about each shared folder on the system, including the share name, path, type, and permissions.

SMB Server Configuration:

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters</mark>

This key holds various settings related to the SMB (Server Message Block) protocol and file sharing, such as security settings, maximum number of users, and other operational parameters.

SMB Client Configuration:

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters</mark>

This key includes settings for the SMB client, controlling how the system accesses shared resources on other computers.
