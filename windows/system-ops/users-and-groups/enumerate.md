# Enumerate

## <mark style="color:red;">Users</mark>

### <mark style="color:purple;">Local</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>whoami</code></mark></td><td>Current user</td></tr><tr><td><mark style="color:yellow;"><code>whoami /priv</code></mark></td><td>Current user privileges</td></tr><tr><td><mark style="color:yellow;"><code>qwinsta</code></mark></td><td>Active user sessions</td></tr><tr><td><mark style="color:yellow;"><code>net session</code></mark></td><td>Current logged on users</td></tr><tr><td><mark style="color:yellow;"><code>psloggedon</code></mark></td><td>Current logged on users</td></tr><tr><td><mark style="color:yellow;"><code>wmic computersystem get username</code></mark></td><td>Current logged on users</td></tr><tr><td><mark style="color:yellow;"><code>net user</code></mark></td><td>User accounts</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance -ClassName Win32_UserAccount</code></mark></td><td>User accounts</td></tr><tr><td><mark style="color:yellow;"><code>Get-LocalUser</code></mark></td><td>User accounts (PowerShell)</td></tr><tr><td><mark style="color:yellow;"><code>Get-WmiObject -Class Win32_UserAccount</code></mark></td><td>User accounts</td></tr><tr><td><mark style="color:yellow;"><code>wmic useraccount get name,sid</code></mark></td><td>SIDs for all users</td></tr><tr><td><mark style="color:yellow;"><code>wmic useraccount where name="USER" get sid</code></mark></td><td>SID for specific user</td></tr><tr><td><mark style="color:yellow;"><code>net user &#x3C;username></code></mark></td><td>User properties</td></tr><tr><td><mark style="color:yellow;"><code>wmic useraccount list /format:list</code></mark></td><td>User properties</td></tr><tr><td><mark style="color:yellow;"><code>wmic useraccount get name,fullname,sid</code></mark></td><td>Specific user properties</td></tr><tr><td><mark style="color:yellow;"><code>net accounts</code></mark></td><td>Default account settings</td></tr></tbody></table>

Retrieves information about a specific user:

```powershell
Get-WmiObject -Class Win32_UserAccount | Where-Object {$_.Name -eq "<username>"} | Select-Object Name, FullName, Description
```

Default username, default domainname, default shell:

```powershell
reg query "HKLM\\Software\\Microsoft\\Windows NT\\CurrentVersion\\Winlogon"
```

### <mark style="color:purple;">Domain</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>net user /domain</code></mark></td><td>Active Directory users</td></tr><tr><td><mark style="color:yellow;"><code>Get-ADUser -Filter *</code></mark></td><td>Active Directory users (requires AD module)</td></tr><tr><td><mark style="color:yellow;"><code>dsquery user</code></mark></td><td>Active Directory users (requires AD)</td></tr></tbody></table>

## <mark style="color:red;">Groups</mark>

### <mark style="color:purple;">Local</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>net localgroup</code></mark></td><td>Groups</td></tr><tr><td><mark style="color:yellow;"><code>Get-LocalGroup</code></mark></td><td>Groups</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup &#x3C;groupName></code></mark></td><td>Group properties</td></tr><tr><td><mark style="color:yellow;"><code>wmic group /format:</code></mark></td><td>Group properties</td></tr><tr><td><mark style="color:yellow;"><code>wmic group where "name='GroupName'" get /format:</code></mark></td><td>Group properties</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup "Users"</code></mark></td><td>Members</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup "Administrators"</code></mark></td><td>Members</td></tr><tr><td><mark style="color:yellow;"><code>Get-LocalGroupMember -Group "Users"</code></mark></td><td>Members</td></tr><tr><td><mark style="color:yellow;"><code>Get-LocalGroupMember -Group "Administrators"</code></mark></td><td>Members</td></tr></tbody></table>

Get all groups:

```powershell
wmic /NAMESPACE:\\root\directory\ldap PATH ds_group GET ds_samaccountname
```

Members of the group:

```powershell
wmic /NAMESPACE:\\root\directory\ldap PATH ds_group where "ds_samaccountname='Domain Admins'" Get ds_member /Value
```

Members of the group:

```powershell
wmic path win32_groupuser where (groupcomponent="win32_group.name="domain admins",domain="DOMAIN_NAME"")
```

### <mark style="color:purple;">Domain</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Get-ADGroupMember -Identity "GroupName"</code></mark></td><td>Domain group members</td></tr><tr><td><mark style="color:yellow;"><code>dsget group "GroupDN" -members</code></mark></td><td>Domain group members</td></tr><tr><td><mark style="color:yellow;"><code>ldapsearch -x -b "dc=example,dc=com" "(objectClass=group)"</code></mark></td><td>AD groups using LDAP search</td></tr><tr><td><mark style="color:yellow;"><code>Get-ADGroup -Filter *</code></mark></td><td>Domain groups</td></tr><tr><td><mark style="color:yellow;"><code>dsquery group</code></mark></td><td>Domain groups</td></tr><tr><td><mark style="color:yellow;"><code>net group</code></mark></td><td>Domain groups</td></tr><tr><td><mark style="color:yellow;"><code>net group /domain</code></mark></td><td>Domain groups</td></tr><tr><td><mark style="color:yellow;"><code>net localgroup administrators /domain</code></mark></td><td>Domain group members</td></tr><tr><td><mark style="color:yellow;"><code>net group "Domain Admins" /domain</code></mark></td><td>Domain groups members</td></tr><tr><td><mark style="color:yellow;"><code>net group "domain computers" /domain</code></mark></td><td>Hosts connected to the domain</td></tr><tr><td><mark style="color:yellow;"><code>net group "Domain Controllers" /domain</code></mark></td><td>DCs</td></tr></tbody></table>
