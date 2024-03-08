# Domain or Workgroup

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="415">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>systeminfo</code></mark></td><td>Extensive system info</td></tr><tr><td><mark style="color:yellow;"><code>systeminfo | findstr /B /C:"Domain"</code></mark></td><td>Retrieves domain or workgroup information from system summary.</td></tr><tr><td><mark style="color:yellow;"><code>get-ciminstance CIM_ComputerSystem</code></mark></td><td>Shows if in Domain or Workgroup, reveals if VM, hostname</td></tr><tr><td><mark style="color:yellow;"><code>get-computerinfo</code></mark></td><td>Extensive system info</td></tr><tr><td><mark style="color:yellow;"><code>echo $env:USERDOMAIN</code></mark></td><td>Get domain name</td></tr><tr><td><mark style="color:yellow;"><code>echo $env:USERDNSDOMAIN</code></mark></td><td>Get FQDN or a domain.</td></tr><tr><td><mark style="color:yellow;"><code>echo $env:logonserver</code></mark></td><td>Get name of the domain controller (Not working for me)</td></tr><tr><td><mark style="color:yellow;"><code>gpresult /V</code></mark></td><td>Get current policy applied</td></tr><tr><td><mark style="color:yellow;"><code>wmic ntdomain list /format:list</code></mark></td><td>Displays information about the Domain and Domain Controllers</td></tr><tr><td><mark style="color:yellow;"><code>wmic computersystem get domain</code></mark></td><td>Displays the domain or workgroup using WMIC.</td></tr><tr><td><mark style="color:yellow;"><code>[System.Environment]::UserDomainName</code></mark></td><td>PowerShell command to display the domain name of the current user.</td></tr><tr><td><mark style="color:yellow;"><code>net config workstation</code></mark></td><td>Shows network configuration including domain or workgroup.</td></tr><tr><td><mark style="color:yellow;"><code>nltest /dclist:&#x3C;DOMAIN></code></mark></td><td>List domain controllers</td></tr></tbody></table>

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
