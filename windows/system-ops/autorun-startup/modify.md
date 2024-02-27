# Modify

## <mark style="color:red;">Scheduled Tasks</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>schtasks /create /sc &#x3C;ScheduleType> /tn &#x3C;TaskName> /tr &#x3C;TaskRun></code></mark></td><td>Creates a scheduled task (CMD).</td></tr><tr><td><mark style="color:yellow;"><code>New-ScheduledTask -Action &#x3C;Action> -Trigger &#x3C;Trigger></code></mark></td><td>Creates a new scheduled task object (PowerShell).</td></tr><tr><td><mark style="color:yellow;"><code>Register-ScheduledTask -TaskName &#x3C;TaskName> -InputObject &#x3C;ScheduledTask></code></mark></td><td>Registers a scheduled task (PowerShell).</td></tr></tbody></table>

## <mark style="color:red;">Registry</mark>

Adds an auto-start entry for the current user (CMD).

{% code overflow="wrap" %}
```powershell
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v <ValueName> /d <ExecutablePath>
```
{% endcode %}

Adds an auto-start entry for all users (CMD).

{% code overflow="wrap" %}
```powershell
reg add "HKLM\Software\Microsoft\Windows\CurrentVersion\Run" /v <ValueName> /d <ExecutablePath>
```
{% endcode %}

Adds an auto-start entry for the current user (PowerShell).

{% code overflow="wrap" %}
```powershell
Set-ItemProperty -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Run' -Name <ValueName> -Value <ExecutablePath>
```
{% endcode %}

Adds an auto-start entry for all users (PowerShell).

{% code overflow="wrap" %}
```powershell
Set-ItemProperty -Path 'HKLM:\Software\Microsoft\Windows\CurrentVersion\Run' -Name <ValueName> -Value <ExecutablePath>
```
{% endcode %}

## <mark style="color:red;">Startup Folder</mark>

Copies a file to the current user's startup folder (CMD).

```powershell
copy <FilePath> "%AppData%\Microsoft\Windows\Start Menu\Programs\Startup\"
```

Copies a file to the current user's startup folder (PowerShell).

{% code overflow="wrap" %}
```powershell
Copy-Item <FilePath> -Destination "$env:APPDATA\Microsoft\Windows\Start Menu\Programs\Startup\"
```
{% endcode %}

## <mark style="color:red;">Services</mark>

Creates a new service set to start automatically (CMD).

```powershell
sc create <ServiceName> binPath= "<PathToExecutable>" start=auto 
```

Creates a new service set to start automatically (PowerShell).

{% code overflow="wrap" %}
```powershell
New-Service -Name <ServiceName> -BinaryPathName "<PathToExecutable>" -StartupType Automatic
```
{% endcode %}

## <mark style="color:red;">Registry Keys</mark>

Registry Query:

```powershell
reg query
```

```powershell
get-itemproperty
```

## <mark style="color:red;">Persistence Keys</mark>

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Run</mark>

Programs in this key run automatically when the current user logs in.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run</mark>

Programs listed here run automatically for all users at system startup.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce</mark>

Commands or programs here run once at the next user login.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce</mark>

Commands or programs in this key run once at the next system startup.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run</mark>

Programs listed here are executed at system startup.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run</mark>

Programs listed here are executed at user login.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon</mark>

Entries such as 'Userinit' and 'Shell' can be modified to run custom scripts or applications during the logon process.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\Load</mark>

Specifies programs to load at user login.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows\Load</mark>

Specifies programs to load at system startup.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\Run</mark>

Specifies additional programs to run at user login.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows\Run</mark>

Specifies additional programs to run at system startup.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellExecuteHooks</mark>

Hooks that can be used to execute code when certain actions occur.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services</mark>

Services listed here are started by the Service Control Manager. Malware can create or modify existing services.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders</mark>

Customization of user shell folders can be used for persistence.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders</mark>

Customization of shell folders at a system-wide level.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components</mark>

Components listed here are executed when a user logs in for the first time and when creating new user accounts.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run</mark>

On 64-bit systems, this key is used to run 32-bit applications at system startup.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Classes\*\ShellEx\ContextMenuHandlers</mark>

Context menu handlers can be used to execute code when certain file types are right-clicked.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Classes\*\ShellEx\ContextMenuHandlers</mark>

Context menu handlers for specific file types under the current user profile.

<mark style="color:blue;">HKLM\Software\Microsoft\Windows\CurrentVersion\Run</mark>

<mark style="color:blue;">HKU\<SID>\Software\Microsoft\Windows\CurrentVersion\Run</mark>

<mark style="color:blue;">HKLM\BCD00000000</mark>

<mark style="color:blue;">HKLM\SAM\SAMs</mark>

## <mark style="color:red;">Startup Folders</mark>

Individual User Startup:

<mark style="color:blue;">C:\Users\<user name>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup</mark>

All Users Statup:

<mark style="color:blue;">C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup</mark>

Are these locations the same across all Windows Versions? Need to research.

## <mark style="color:red;">Sysinternals</mark>

| <mark style="color:yellow;">`autorunsc -accepteula`</mark> | Start                             |
| ---------------------------------------------------------- | --------------------------------- |
| <mark style="color:yellow;">`autorunsc -a`</mark>          | (all) # ALWAYS CHECK BOOT EXECUTE |
| <mark style="color:yellow;">`autorunsc -s`</mark>          | Services                          |
| <mark style="color:yellow;">`autorunsc -t`</mark>          | Tasks                             |
| <mark style="color:yellow;">`autorunsc -b`</mark>          | Boot execute                      |
| <mark style="color:yellow;">`autorunsc -d`</mark>          | App init DLLs                     |
