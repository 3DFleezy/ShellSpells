# Page

## <mark style="color:red;">File Permissions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>icacls "file.txt" /grant "username:R"</code></mark></td><td>Grants read (R) permissions to the specified user.</td></tr><tr><td><mark style="color:yellow;"><code>icacls "file.txt" /grant "username:F"</code></mark></td><td>Grants full control (F) permissions to the specified user.</td></tr><tr><td><mark style="color:yellow;"><code>icacls "file.txt" /remove "username"</code></mark></td><td>Removes all explicitly set permissions for the user.</td></tr><tr><td><mark style="color:yellow;"><code>icacls "file.txt" /deny "username:W"</code></mark></td><td>Denies write (W) permission to the specified user.</td></tr><tr><td><mark style="color:yellow;"><code>icacls "file.txt" /reset</code></mark></td><td>Resets the permissions for "file.txt" to inherit from its parent directory.</td></tr><tr><td><mark style="color:yellow;"><code>icacls "C:\folder" /grant "username:M" /T</code></mark></td><td>Grants modify (M) permissions to "username" on the folder and all its subfolders and files.</td></tr><tr><td><mark style="color:yellow;"><code>icacls "file.txt" /save "C:\path\to\acls.txt"</code></mark></td><td>Saves the Access Control List (ACL) of "file.txt" to "acls.txt".</td></tr><tr><td><mark style="color:yellow;"><code>icacls "C:\folder" /restore "C:\path\to\acls.txt"</code></mark></td><td>Restores the ACLs to the files in "folder" from "acls.txt".</td></tr><tr><td><mark style="color:yellow;"><code>icacls &#x3C;FilePathOrDirectory> /inheritance:r</code></mark></td><td>Removes inherited permissions from a file or directory.</td></tr><tr><td><mark style="color:yellow;"><code>icacls &#x3C;FilePathOrDirectory> /setowner &#x3C;UserOrGroup></code></mark></td><td>Changes the owner of a file or directory.</td></tr><tr><td><mark style="color:yellow;"><code>takeown /f C:\&#x3C;filename>.exe</code></mark></td><td>If you have SeTakeOwnership, you can own a process or file.</td></tr></tbody></table>

Grant permissions:

```powershell
Set-Acl <file_or_folder> -AclObject (Get-Acl <file_or_folder>).Access | Add-AclEntry <username>:(R,W,X)
```

Revoke permissions:

```powershell
Set-Acl <file_or_folder> -AclObject (Get-Acl <file_or_folder>).Access | Remove-AclEntry <username>
```

Change owner:

```powershell
Set-Acl <file_or_folder> -Owner <username>
```

### <mark style="color:purple;">Graphical User Interface (GUI)</mark>

File/Folder Properties:

Right-click the file or folder, select "Properties."

Go to the "Security" tab.

Click "Edit" to modify permissions.

Add, remove, or change permissions for users or groups.

Permissions Syntax: Use abbreviations for permissions:

| Permission | Description    |
| ---------- | -------------- |
| F          | Full control   |
| M          | Modify         |
| RX         | Read & execute |
| R          | Read           |
| W          | Write          |

## <mark style="color:red;">User Permissions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>net user &#x3C;Username> &#x3C;Password> /add</code></mark></td><td>Creates a new user account with a password.</td></tr><tr><td><mark style="color:yellow;"><code>net user &#x3C;Username> /delete</code></mark></td><td>Deletes a user account.</td></tr><tr><td><mark style="color:yellow;"><code>net user &#x3C;username> /active:no</code></mark></td><td>Disables account.</td></tr><tr><td><mark style="color:yellow;"><code>net user &#x3C;username> /active:yes</code></mark></td><td>Enables account.</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup &#x3C;group_name> &#x3C;username> /add</code></mark></td><td>Adds user to group.</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup &#x3C;group_name> &#x3C;username> /delete</code></mark></td><td>Removes user from group.</td></tr></tbody></table>

## <mark style="color:red;">Group Permissions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>net localgroup &#x3C;GroupName> &#x3C;Username> /add</code></mark></td><td>Adds a user to a local group.</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup &#x3C;GroupName> &#x3C;Username> /delete</code></mark></td><td>Removes a user from a local group.</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup &#x3C;GroupName> /add</code></mark></td><td>Creates a new local group.</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup &#x3C;GroupName> /delete</code></mark></td><td>Deletes a local group.</td></tr><tr><td><mark style="color:yellow;"><code>Add-LocalGroupMember -Group "&#x3C;group_name>" -Member "&#x3C;username>"</code></mark></td><td>Add member to group</td></tr><tr><td><mark style="color:yellow;"><code>Remove-LocalGroupMember -Group "&#x3C;group_name>" -Member "&#x3C;username>"</code></mark></td><td>Remove member from group</td></tr><tr><td><mark style="color:yellow;"><code>Add-ADGroupMember</code></mark></td><td>AD add member</td></tr><tr><td><mark style="color:yellow;"><code>Remove-ADGroupMember</code></mark></td><td>AD remove member</td></tr></tbody></table>

### <mark style="color:purple;">Graphical User Interface (GUI):</mark>

Local Users and Groups (Windows 10 Pro and above):

Open Computer Management (right-click "This PC" > "Manage").

Go to "Local Users and Groups" > "Groups."

Right-click the group you want to modify and select "Properties."

Go to the "Members" tab.

Add or remove users as needed.

## <mark style="color:red;">Share Permissions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;">`net share &#x3C;share_name> /grant:,&#x3C;READ</mark></td><td>CHANGE</td></tr><tr><td><mark style="color:yellow;"><code>net share &#x3C;ShareName> /delete</code></mark></td><td>Deletes a shared folder.</td></tr><tr><td><mark style="color:yellow;"><code>icacls &#x3C;FolderPath> /grant &#x3C;UserOrGroup>:&#x3C;Permission></code></mark></td><td>Modifies NTFS permissions for the shared folder.</td></tr><tr><td><mark style="color:yellow;"><code>New-SmbShare -Name &#x3C;ShareName> -Path &#x3C;FolderPath> -FullAccess &#x3C;UserOrGroup></code></mark></td><td>Creates a new SMB share with Full Access permissions (PowerShell).</td></tr><tr><td><mark style="color:yellow;"><code>Remove-SmbShare -Name &#x3C;ShareName></code></mark></td><td>Removes an SMB share (PowerShell).</td></tr><tr><td><mark style="color:yellow;"><code>Grant-SmbShareAccess</code></mark></td><td>Grants permissions to users or groups on a share.</td></tr><tr><td><mark style="color:yellow;"><code>Revoke-SmbShareAccess</code></mark></td><td>Revokes permissions from users or groups.</td></tr><tr><td><mark style="color:yellow;"><code>Remove-SmbShare</code></mark></td><td>Deletes a share.</td></tr></tbody></table>

## <mark style="color:red;">Registry Locations</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\SpecialAccounts\UserList</mark>

Controls the visibility of user accounts on the Welcome screen. Can be used to hide specific user accounts.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Shares</mark>

Contains information about shared folders, including share permissions.

<mark style="color:blue;">HKEY\_CLASSES\_ROOT</mark>

Contains file associations and COM object registrations, which include permissions for these objects.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System</mark>

Stores system-level policies, including user rights assignments and security options.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurePipeServers\winreg</mark>

Controls permissions for remote access to the registry.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList</mark>

Contains information about user profiles, including profile paths and permissions.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\FolderDescriptions</mark>

Defines known folders in Windows, including paths and permissions.
