# System Details

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>systeminfo</code></mark></td><td>Extensive system info</td></tr><tr><td><mark style="color:yellow;"><code>get-computerinfo</code></mark></td><td>Extensive system info</td></tr><tr><td><mark style="color:yellow;"><code>ver</code></mark></td><td>System version (CMD only)</td></tr><tr><td><mark style="color:yellow;"><code>net view</code></mark></td><td>ServerName and Remarks of computers in your current domain</td></tr><tr><td><mark style="color:yellow;"><code>hostname</code></mark></td><td>Hostname</td></tr><tr><td><mark style="color:yellow;"><code>net statistics</code></mark></td><td>Options for statistics</td></tr><tr><td><mark style="color:yellow;"><code>net statistics Workstation</code></mark></td><td>Uptime, and network statistics for workstation</td></tr><tr><td><mark style="color:yellow;"><code>wmic os get caption</code></mark></td><td>OS Name</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance -ClassName Win32_ComputerSystem</code></mark></td><td>General system info</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance -ClassName Win32_OperatingSystem</code></mark></td><td>OS</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance -ClassName Win32_LogicalDisk</code></mark></td><td>Logical disks</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance -ClassName Win32_NetworkAdapter</code></mark></td><td>Network adapters</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance -ClassName Win32_Product</code></mark></td><td>Installed software</td></tr></tbody></table>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem | select name,domain | fl
```

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem | select SystemDirectory, BuildNumber, Version | fl
```

OS Name and Service Pack:

```powershell
reg query "HKLM\\Software\\Microsoft\\Windows NT\\CurrentVersion" 
```

Service Pack (Recursive):

```powershell
reg query hklm /v CSDVersion /s
```

Service Pack Info:

```powershell
wmic os get servicepackmajorversion
```

Shutdown time ? (System directory, shell error mode, CSDversion/CSDReleaseType)

```powershell
reg.exe query HKLM\System\CurrentControlSet\Control\Windows
```

Show shell, default domain name, default user name, legal notice, etc.:

```powershell
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon"
```

## GUI Commands and Locations

Run dialog: <mark style="color:yellow;">`msinfo32`</mark>

Opens system info in the GUI

System Control Panel:

Press Win + X and select "System". This provides basic system information like Windows edition, system type, etc.

Control Panel:

Navigate to Control Panel > System and Security > System. This provides basic information about your computer.

Task Manager:

Open Task Manager (Ctrl + Shift + Esc) and navigate to the Performance tab to view CPU, memory, disk, and network usage.

Device Manager:

Open Device Manager by pressing Win + X and selecting "Device Manager". This allows you to view and manage hardware devices.

Open the Run dialog (Win + R) and type dxdiag. This provides information about DirectX components and system information.

## Registry Locations

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\HARDWARE\DESCRIPTION\System</mark>

Contains detailed system hardware information.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion</mark>

Stores Windows version, build, product name, and installation information.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SystemInformation</mark>

Holds system manufacturer, model, and type information.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Enum</mark>

Enumerates all hardware devices and their configuration.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services</mark>

Lists all system services and their configurations.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion</mark>

Contains various Windows settings, including installed software and system policies.
