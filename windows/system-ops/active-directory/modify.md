# Modify

## Commands

<table data-header-hidden data-full-width="true"><thead><tr><th width="375">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>dsmod user</code></mark></td><td>Modifies properties of a user account.</td></tr><tr><td><mark style="color:yellow;"><code>dsmod group</code></mark></td><td>Modifies properties of a group.</td></tr><tr><td><mark style="color:yellow;"><code>dsmod computer</code></mark></td><td>Modifies properties of a computer object.</td></tr><tr><td><mark style="color:yellow;"><code>dsadd</code></mark></td><td>Adds objects to Active Directory, such as users, groups, or organizational units.</td></tr><tr><td><mark style="color:yellow;"><code>dsmod</code></mark></td><td>Modifies properties of Active Directory objects.</td></tr><tr><td><mark style="color:yellow;"><code>dsrm</code></mark></td><td>Removes Active Directory objects.</td></tr><tr><td><mark style="color:yellow;"><code>dsquery</code></mark></td><td>Queries Active Directory for objects that match specified criteria.</td></tr><tr><td><mark style="color:yellow;"><code>ldifde</code></mark></td><td>Imports and exports data to and from Active Directory using LDIF (LDAP Data Interchange Format).</td></tr><tr><td><mark style="color:yellow;"><code>csvde</code></mark></td><td>Imports and exports data to and from Active Directory using CSV (Comma-Separated Values) files.</td></tr><tr><td><mark style="color:yellow;"><code>ntdsutil</code></mark></td><td>A command-line utility for managing various aspects of Active Directory, including metadata cleanup and database maintenance.</td></tr><tr><td><mark style="color:yellow;"><code>adprep</code></mark></td><td>Used for preparing a forest and domain for the introduction of a new version of Windows Server.</td></tr><tr><td><mark style="color:yellow;"><code>netdom</code></mark></td><td>A tool for managing computer accounts, trust relationships, and joining or disjoining computers from domains.</td></tr><tr><td><mark style="color:yellow;"><code>Set-ADUser</code></mark></td><td>Modifying user account properties in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>Set-ADGroup</code></mark></td><td>Modifying group properties in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>Set-ADComputer</code></mark></td><td>Modifying computer object properties in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>New-ADUser</code></mark></td><td>Creating new user accounts in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>New-ADGroup</code></mark></td><td>Creating new groups in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>New-ADOrganizationalUnit</code></mark></td><td>Creating new organizational units in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>Remove-ADObject</code></mark></td><td>Removing Active Directory objects.</td></tr><tr><td><mark style="color:yellow;"><code>Move-ADObject</code></mark></td><td>Moving Active Directory objects between organizational units.</td></tr><tr><td><mark style="color:yellow;"><code>Enable-ADAccount</code></mark></td><td>Enabling disabled user accounts.</td></tr><tr><td><mark style="color:yellow;"><code>Disable-ADAccount</code></mark></td><td>Disabling user accounts.</td></tr><tr><td><mark style="color:yellow;"><code>Add-ADGroupMember</code></mark></td><td>Adding members to groups in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>Remove-ADGroupMember</code></mark></td><td>Removing members from groups in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>Add-ADPrincipalGroupMembership</code></mark></td><td>Adding users to groups in Active Directory.</td></tr><tr><td><mark style="color:yellow;"><code>Remove-ADPrincipalGroupMembership</code></mark></td><td>Removing users from groups in Active Directory.</td></tr></tbody></table>

## Guest Account

Enable guest account:

```powershell
Enable-ADaccount -Identity guest
```

Set guest account password. Blank password:

```powershell
set-adaccountpassword -identity guest
```

Add guest to "Domain Admins group":

```powershell
Add ADGroupMember -Identity "Domain Admins" -Members guest
```

If guest password was set:

```powershell
get-aduser -filter Distinguishedname
```

Create account with no password

```powershell
New-ADUser -Name "bad guy" -Passwordnotrequired 1 -path  "copy from get-aduser"
```

Set the password:

```powershell
set-adaccountpassword -identity "bad guy"
```

Enable account:

```powershell
Enable-ADaccount -Identity "bad guy"
```

Add to "Domain Admins group":

```powershell
Add ADGroupMember -Identity "Domain Admins" -Members "bad guy"
```

Remove from "Domain Admins group":

```powershell
remove-aduser -identity "domain admins" -members "bad guy"
```

Disable guest account:

```powershell
disable-adaccount -identity guest
```

## Add Objects

### Users:

Add User and set properties:

{% code overflow="wrap" %}
```powershell
dsadd user "CN=NewUser,OU=Users,DC=example,DC=com" -samid <SAMacctName -upn NewUser@example.com -fn <firstname> -ln <lastname> -display "<DisplayName>" -pwd Password123
```
{% endcode %}

<mark style="color:yellow;">`"CN=NewUser,OU=Users,DC=example,DC=com"`</mark> specifies the distinguished name (DN) of the new user.

<mark style="color:yellow;">`-samid NewUser`</mark> sets the SamAccountName for the user.

<mark style="color:yellow;">`-upn NewUser@example.com`</mark> sets the User Principal Name (UPN) for the user.

<mark style="color:yellow;">`-fn [firstname]`</mark> specifies the first name of the user.

<mark style="color:yellow;">`-ln [lastname]`</mark> specifies the last name of the user.

<mark style="color:yellow;">`-display "[DisplayName]"`</mark> sets the display name for the user.

<mark style="color:yellow;">`-pwd Password123`</mark> specifies the initial password for the user.



Adding a User Using Command Prompt (CMD):

```powershell
net user NewUser Password123 /add /domain
```

Adding a User Using PowerShell (New-ADUser cmdlet from RSAT):

{% code overflow="wrap" %}
```powershell
New-ADUser -Name "NewUser" -AccountPassword (ConvertTo-SecureString "Password123" -AsPlainText -Force) -Enabled $true -PasswordNeverExpires $true
```
{% endcode %}

Adding a User Using PowerShell (Add-ADUser cmdlet from RSAT):

{% code overflow="wrap" %}
```powershell
Add-ADUser -Name "NewUser" -AccountPassword (ConvertTo-SecureString "Password123" -AsPlainText -Force) -Enabled $true -PasswordNeverExpires $true
```
{% endcode %}

Adding a User Using Get-CimInstance (PowerShell WMI):

```
powershell
$UserClass = [WMIClass]("\\Domain\root\directory\LDAP").CreateInstance()
$UserClass.FullName = "CN=NewUser,CN=Users,DC=example,DC=com"
$UserClass.SamAccountName = "NewUser"
$UserClass.UserPrincipalName = "NewUser@example.com"
$UserClass.SetPassword("Password123")
$UserClass.Put()
```

Add user using WMIC:

{% code overflow="wrap" %}
```powershell
wmic /namespace:\\root\directory\ldap path ds_user call createuser "CN=NewUser,CN=Users,DC=example,DC=com","Password123"
```
{% endcode %}

### Groups:

Add new group:

```powershell
dsadd group "CN=NewGroup,OU=Groups,DC=example,DC=com" 
```

Adding a Group Using PowerShell (New-ADGroup cmdlet from RSAT):

```powershell
New-ADGroup -Name "NewGroup"
```

Add Member:

{% code overflow="wrap" %}
```powershell
dsmod group "CN=HRGroup,OU=Groups,DC=example,DC=com" -addmbr "CN=John Doe,OU=Users,DC=example,DC=com"
```
{% endcode %}

### Computer:

Adding a Computer Using Command Prompt (CMD):

```powershell
net computer NewComputer /add /domain
```

Adding a Computer Using PowerShell (Add-ADComputer cmdlet from RSAT):

```powershell
Add-ADComputer -Name "NewComputer"
```

### OU:

Adding an Organizational Unit (OU) Using PowerShell (New-ADOrganizationalUnit cmdlet from RSAT):

```powershell
New-ADOrganizationalUnit -Name "NewOU"
```

### Printer:

Adding a Printer Using PowerShell (Add-Printer cmdlet):

{% code overflow="wrap" %}
```
powershell
Add-Printer -Name "NewPrinter" -PortName "IP_192.168.1.100" -DriverName "HP Universal Print Driver" -Shared $true
```
{% endcode %}

### Share:

Adding a Shared Folder Using PowerShell (New-SmbShare cmdlet):

{% code overflow="wrap" %}
```powershell
New-SmbShare -Name "SharedFolder" -Path "C:\SharedFolder" -FullAccess "Domain\NewUser"
```
{% endcode %}

### DNS Record:

Adding a DNS Record Using PowerShell (Add-DnsServerResourceRecordA cmdlet):

{% code overflow="wrap" %}
```powershell
Add-DnsServerResourceRecordA -ZoneName "example.com" -Name "NewHost" -IPv4Address "192.168.1.100" -AllowUpdateAny
```
{% endcode %}

### Certificates:

Adding a Certificate Using PowerShell (Import-PfxCertificate cmdlet):

{% code overflow="wrap" %}
```powershell
Import-PfxCertificate -FilePath "C:\NewCertificate.pfx" -CertStoreLocation "Cert:\LocalMachine\My"
```
{% endcode %}

## Modify Objects

### Users:

Change User Password:

```powershell
dsmod user "CN=John Doe,OU=Users,DC=example,DC=com" -pwd Password123
```

Change User description:

```powershell
dsmod user "CN=Jane Smith,OU=Users,DC=example,DC=com" -desc "New Description"
```

### Groups:

Change Description:

```powershell
dsmod group "CN=SalesGroup,OU=Groups,DC=example,DC=com" -desc "New Description"
```

## Delete Objects

### Users:

User from the "Users" Container:

```powershell
dsrm "CN=John Doe,OU=Users,DC=example,DC=com"
```

### Group from the "Groups" Organizational Unit:

```powershell
dsrm "CN=ObsoleteGroup,OU=Groups,DC=example,DC=com"
```

### Deleting an Organizational Unit (OU):

```powershell
dsrm "OU=ObsoleteOU,DC=example,DC=com"
```

### Computer Object:

```powershell
dsrm "CN=Workstation123,OU=Computers,DC=example,DC=com"
```

### Contact Object:

```powershell
dsrm "CN=ContactPerson,OU=Contacts,DC=example,DC=com"
```

### Printer Object:

```powershell
dsrm "CN=PrinterX,OU=Printers,DC=example,DC=com"
```

### Security Group:

```powershell
dsrm "CN=SecurityGroup,OU=Groups,DC=example,DC=com"
```

### Distribution Group:

```powershell
dsrm "CN=DistributionGroup,OU=Groups,DC=example,DC=com"
```

### Application Object:

```powershell
dsrm "CN=AppServer,OU=Servers,DC=example,DC=com"
```

### Exchange Mailbox:

```powershell
dsrm "CN=MailboxUser,OU=Users,DC=example,DC=com"
```
