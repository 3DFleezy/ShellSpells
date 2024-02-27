# Enumerate

## <mark style="color:red;">File Permissions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>icacls &#x3C;FilePath></code></mark></td><td>Displays or modifies DACLs on specified files (CMD).</td></tr><tr><td><mark style="color:yellow;"><code>cacls &#x3C;FilePathOrDirectory></code></mark></td><td>(Deprecated) Displays the ACL for files and directories.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Acl -Path &#x3C;FilePathOrDirectory></code></mark></td><td>Gets the ACL for a specific file or directory.</td></tr></tbody></table>

Displays a detailed list of ACL entries for a specific file or directory:

```powershell
Get-Acl -Path <FilePathOrDirectory> | Format-List
```

Lists access rules for a file or directory:

```powershell
Get-Acl -Path <FilePathOrDirectory> | Select-Object -ExpandProperty Access
```

Retrieves the ACL for all files and directories within a specified path recursively:

```powershell
Get-ChildItem -Path <DirectoryPath> -Recurse | Get-Acl
```

Retrieves file names, paths, and access masks (numeric representation of permissions):

```powershell
wmic datafile where (Path='<path>\<filename>') get Name, FileName, AccessMask
```

Displays permissions in a more concise format, listing each user or group and their corresponding permissions:

{% code overflow="wrap" %}
```powershell
Get-Acl -Path <path>\<filename> | Select-Object -ExpandProperty Access | ForEach-Object {$_.IdentityReference; $_.FileSystemRights}
```
{% endcode %}

Leverages the AccessToString() method to directly convert access masks to human-readable permission strings.

{% code overflow="wrap" %}
```powershell
Get-Acl -Path <path>\<filename> | Select-Object -ExpandProperty Access | ForEach-Object { $_.IdentityReference; $_.FileSystemRights.ToString() }
```
{% endcode %}

#### <mark style="color:green;">Understanding access masks:</mark>

Numeric values represent permissions (e.g., 2032127 = Full Control).

Use PowerShell's <mark style="color:yellow;">`Get-Acl`</mark> and <mark style="color:yellow;">`AccessToString`</mark> methods to convert them to human-readable format.

Filtering by permission level:

Use PowerShell's <mark style="color:yellow;">`Where-Object`</mark> cmdlet to filter based on access mask values or specific permissions.

Tools for advanced analysis:

Consider tools like AccessEnum or NTFS Permissions Reporter for detailed permission analysis and reporting.

## <mark style="color:red;">User Permissions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>whoami /priv</code></mark></td><td>Displays current user privileges.</td></tr><tr><td><mark style="color:yellow;"><code>net user &#x3C;username></code></mark></td><td>Displays basic information about a user.</td></tr><tr><td><mark style="color:yellow;"><code>Get-LocalUser</code></mark></td><td>Retrieves local user accounts.</td></tr><tr><td><mark style="color:yellow;"><code>Get-LocalGroupMember &#x3C;GroupName></code></mark></td><td>Retrieves members of a local group.</td></tr><tr><td><mark style="color:yellow;"><code>icacls &#x3C;file_or_folder></code></mark></td><td>Displays user permissions for a file or folder.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ADUser -Filter * -Properties *</code></mark></td><td>Retrieves user accounts from Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ADGroupMember &#x3C;GroupName></code></mark></td><td>Retrieves members of an Active Directory group.</td></tr></tbody></table>

Retrieves information about a specific user:

{% code overflow="wrap" %}
```powershell
Get-WmiObject -Class Win32_UserAccount | Where-Object {$_.Name -eq "<username>"} | Select-Object Name, FullName, Description
```
{% endcode %}

## <mark style="color:red;">Group Permissions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Get-LocalGroup</code></mark></td><td>Retrieves local groups on a computer.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ADGroup -Filter * -Properties *</code></mark></td><td>Retrieves groups from Active Directory (requires AD module).</td></tr><tr><td><mark style="color:yellow;"><code>Get-LocalGroupMember &#x3C;GroupName></code></mark></td><td>Retrieves members of a local group.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ADGroupMember &#x3C;GroupName></code></mark></td><td>Retrieves members of an Active Directory group (requires AD).</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup &#x3C;group_name></code></mark></td><td>Lists members of a local group without detailed permissions.</td></tr><tr><td><mark style="color:yellow;"><code>icacls &#x3C;file_or_folder></code></mark></td><td>Displays permissions for a file or folder, including groups.</td></tr><tr><td><mark style="color:yellow;"><code>whoami /groups</code></mark></td><td>Shows the groups to which the current user belongs.</td></tr></tbody></table>

## <mark style="color:red;">Share Permissions</mark>

{% code overflow="wrap" %}
```powershell
Get-WmiObject Win32_LogicalShareSecuritySetting `| Retrieves share permissions (PowerShell).
```
{% endcode %}

Enumerates user permissions on a network share:

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_LogicalShareSecuritySetting | Where-Object {$_.Name -eq "<share_name>"} | Get-CimAssociatedInstance -ResultClassName Win32_Ace | Select-Object Principal, AccessMask
```
{% endcode %}

## <mark style="color:red;">Sysinternals</mark>

<mark style="color:yellow;">`AccessChk`</mark> A command-line tool for viewing effective permissions on files, registry keys, services, processes, and more

