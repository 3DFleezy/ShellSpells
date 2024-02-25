# Domain or Workgroup

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="415">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systeminfo</code></td><td>Extensive system info</td></tr><tr><td><code>systeminfo | findstr /B /C:"Domain"</code></td><td>Retrieves domain or workgroup information from system summary.</td></tr><tr><td><code>get-computerinfo</code></td><td>Extensive system info</td></tr><tr><td><code>echo $env:USERDOMAIN</code></td><td>Get domain name</td></tr><tr><td><code>echo $env:USERDNSDOMAIN</code></td><td>Get FQDN or a domain.</td></tr><tr><td><code>echo $env:logonserver</code></td><td>Get name of the domain controller (Not working for me)</td></tr><tr><td><code>gpresult /V</code></td><td>Get current policy applied</td></tr><tr><td><code>wmic ntdomain list /format:list</code></td><td>Displays information about the Domain and Domain Controllers</td></tr><tr><td><code>wmic computersystem get domain</code></td><td>Displays the domain or workgroup using WMIC.</td></tr><tr><td><code>[System.Environment]::UserDomainName</code></td><td>PowerShell command to display the domain name of the current user.</td></tr><tr><td><code>net config workstation</code></td><td>Shows network configuration including domain or workgroup.</td></tr><tr><td><code>nltest /dclist:&#x3C;DOMAIN></code></td><td>List domain controllers</td></tr></tbody></table>

PowerShell command to get domain or workgroup via WMI.

```powershell
Get-WmiObject Win32_ComputerSystem | Select-Object Domain 
```

```powershell
reg query "HKLM\system\currentcontrolset\services\tcpip\parameters"
```

Look for "NV Domain key". Next, see the systeminfo output. What is the value of the "Domain" field?

If the NV Domain key doesn't exist or exists and is empty = definitely workgroup.

If there's something in NV Domain and it matches systeminfo = definitely domain.

If there's something in NV Domain and it does _not_ match systeminfo = definitely workgroup.

## <mark style="color:red;">Registry Locations</mark>

Domain Information:

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</mark> \
The Domain value in this key shows the domain name of the computer.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon</mark> \
The DefaultDomainName value holds the default domain name used for login. Workgroup Information:

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</mark> \
The NV Hostname value in this key represents the computer's name in the workgroup.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\ComputerName\ActiveComputerName</mark> \
The ComputerName value contains the active computer name, which is used in the workgroup.
