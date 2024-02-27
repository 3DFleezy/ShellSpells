# PowerShell Config

## Version

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>get-host | select-object Version</code></mark></td><td>Get PowerShell version using <code>get-host</code>.</td></tr><tr><td><mark style="color:yellow;"><code>echo $PSVERSIONTABLE</code></mark></td><td>Shows all version and build information.</td></tr><tr><td><mark style="color:yellow;"><code>$PSVersionTable.PSVersion</code></mark></td><td>Get PowerShell version using <code>$PSVersionTable.PSVersion</code>.</td></tr><tr><td><mark style="color:yellow;"><code>powershell -command "$PSVersionTable.PSVersion"</code></mark></td><td>Get PowerShell version in Command Prompt.</td></tr></tbody></table>

Queries the installed versions of PowerShell using Common Information Model (CIM) and filters based on the product name:

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_Product -Filter "Name LIKE 'Microsoft PowerShell%'" | Select-Object -Property Name, Version
```
{% endcode %}

Retrieves the PowerShell version as part of the operating system information using CIM:

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object -Property PSVersion
```
{% endcode %}

Lists installed versions of PowerShell using (WMI):

```powershell
wmic product where "Name like 'Microsoft PowerShell%'" get Name, Version 
```

Retrieves the PowerShell version as part of the operating system information using WMIC:

```powershell
wmic os get PowerShellVersion
```

## PowerShell Profiles

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>$PsHome</code></mark></td><td>Stores the installation directory for PowerShell.</td></tr><tr><td><mark style="color:yellow;"><code>$Home</code></mark></td><td>Stores the current user’s home directory.</td></tr><tr><td><mark style="color:yellow;"><code>$PROFILE</code></mark></td><td>Stores the path to the current user's profile script.</td></tr><tr><td><mark style="color:yellow;"><code>ISE $profile</code></mark></td><td>Opens the user's profile script in the Integrated Scripting Environment (ISE).</td></tr><tr><td><mark style="color:yellow;"><code>$PsHome\\Profile.ps1</code></mark></td><td>Profile script for all users and all hosts.</td></tr><tr><td><mark style="color:yellow;"><code>$PsHome\\Microsoft.PowerShell_profile.ps1</code></mark></td><td>Profile script for all users on the current host.</td></tr><tr><td><mark style="color:yellow;"><code>$Home\\[My]Documents\\Profile.ps1</code></mark></td><td>Profile script for the current user and all hosts.</td></tr><tr><td><mark style="color:yellow;"><code>$Home\\[My]Documents\\WindowsPowerShell\\Profile.ps1</code></mark></td><td>Profile script for the current user on the current host.</td></tr><tr><td><mark style="color:yellow;"><code>$profile | Get-Member -Type NoteProperty</code></mark></td><td>Displays the profile values of Names, MemberType, and Paths.</td></tr><tr><td><mark style="color:yellow;"><code>$Profile | get-member -type noteproperty | ft -wrap</code></mark></td><td>Displays the profile values with wrapped text.</td></tr><tr><td><mark style="color:yellow;"><code>$PROFILE | Get-Member -MemberType noteproperty | select name</code></mark></td><td>Displays only the Names of profile properties.</td></tr><tr><td><mark style="color:yellow;"><code>Test-Path -Path $profile.currentUsercurrentHost</code></mark></td><td>Checks if the profile for the current user and host exists.</td></tr><tr><td><mark style="color:yellow;"><code>Test-Path -Path $profile.currentUserAllHosts</code></mark></td><td>Checks if the profile for the current user and all hosts exists.</td></tr><tr><td><mark style="color:yellow;"><code>Test-Path -Path $profile.AllUsersAllHosts</code></mark></td><td>Checks if the profiles for all users and all hosts exist.</td></tr><tr><td><mark style="color:yellow;"><code>Test-Path -Path $profile.AllUserscurrentHost</code></mark></td><td>Checks if the profiles for all users on the current host exist.</td></tr><tr><td><mark style="color:yellow;"><code>New-Item -ItemType File -Path $profile -Force</code></mark></td><td>Creates a new profile script for the current user, ignoring errors.</td></tr></tbody></table>

## Switch Versions

Switch to PSv7:

<mark style="color:yellow;">`pwsh`</mark>

## PowerShell Execution Policy

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Get-ExecutionPolicy -list</code></mark></td><td>Lists all of the Scopes and ExecutionPolicies on the system.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ExecutionPolicy</code></mark></td><td>Gets the current user's ExecutionPolicy.</td></tr><tr><td><mark style="color:yellow;"><code>powershell.exe Get-ExecutionPolicy</code></mark></td><td>Retrieves the current PowerShell execution policy using CMD.</td></tr></tbody></table>

Sets the ExecutionPolicy for the CurrentUser to Unrestricted:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser 
```

Queries the registry for the execution policy setting:

{% code overflow="wrap" %}
```powershell
reg query "HKLM\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.PowerShell" /v ExecutionPolicy
```
{% endcode %}

Retrieves the execution policy setting from the registry:

{% code overflow="wrap" %}
```powershell
Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.PowerShell" -Name ExecutionPolicy
```
{% endcode %}

Generates an HTML report containing the Group Policy settings, including the PowerShell execution policy, and opens it in the default web browser:

```powershell
gpresult /h result.html && start result.html
```

## Notes

<mark style="color:green;">Restricted:</mark>\
No scripts are allowed to run, offering the highest security level.\
Useful for locked-down environments or when testing untrusted code.

<mark style="color:green;">AllSigned:</mark>\
Requires all scripts and configuration files, even those written locally, to be signed by a trusted publisher before execution.\
Provides strong security but requires additional setup for signing your own scripts.

<mark style="color:green;">RemoteSigned:</mark>\
Permits execution of scripts downloaded from the internet only if they are signed by a trusted publisher.\
Offers a balance between security and functionality, allowing some remote script execution.

<mark style="color:green;">Bypass:</mark>\
No restrictions are in place, allowing all scripts to run without warnings or prompts.\
Least secure option, use with caution only in trusted environments.

<mark style="color:green;">Default:</mark>\
Sets the execution policy to the default for your system, which is:\
Restricted for Windows client operating systems.\
RemoteSigned for Windows server operating systems.
