# Hardware & Resources

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="714">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>Get-CimInstance -ClassName Win32_ComputerSystem</code></td><td>System Info</td></tr><tr><td><code>Get-WmiObject -Class Win32_ComputerSystem</code></td><td>Computer info</td></tr><tr><td><code>Get-WmiObject -Class Win32_OperatingSystem</code></td><td>OS</td></tr><tr><td><code>Get-CimInstance -ClassName Win32_OperatingSystem</code></td><td>OS</td></tr><tr><td><code>wmic os get Caption,Version,OSArchitecture,LastBootUpTime</code></td><td>OS</td></tr><tr><td><code>wmic cpu get Caption, Name, NumberOfCores, NumberOfLogicalProcessors</code></td><td>CPU</td></tr><tr><td><code>Get-CimInstance -ClassName Win32_Processor</code></td><td>CPU</td></tr><tr><td><code>Get-WmiObject -Class Win32_Processor</code></td><td>CPU</td></tr><tr><td><code>wmic bios get Manufacturer,Name,SerialNumber,Version</code></td><td>BIOS</td></tr><tr><td><code>Get-CimInstance -ClassName Win32_BIOS</code></td><td>BIOS</td></tr><tr><td><code>Get-WmiObject -Class Win32_BIOS</code></td><td>BIOS</td></tr><tr><td><code>wmic memorychip get BankLabel,Capacity,Speed</code></td><td>Physical Memory</td></tr><tr><td><code>Get-CimInstance -ClassName Win32_PhysicalMemory</code></td><td>Physical Memory</td></tr><tr><td><code>Get-WmiObject -Class Win32_PhysicalMemory</code></td><td>Physical Memory</td></tr><tr><td><code>wmic diskdrive get Model,Size,MediaType</code></td><td>Disk Drives</td></tr><tr><td><code>Get-CimInstance -ClassName Win32_DiskDrive</code></td><td>Disk Drives</td></tr><tr><td><code>Get-WmiObject -Class Win32_DiskDrive</code></td><td>Disk Drives</td></tr><tr><td><code>wmic baseboard get Manufacturer,Product,SerialNumber,Version</code></td><td>Motherboard</td></tr><tr><td><code>Get-CimInstance -ClassName Win32_BaseBoard</code></td><td>Motherboard</td></tr><tr><td><code>Get-WmiObject -Class Win32_BaseBoard</code></td><td>Motherboard</td></tr><tr><td><code>wmic nic get Caption,Name,NetConnectionStatus,Speed,MACAddress</code></td><td>Network Adapters</td></tr><tr><td><code>Get-CimInstance -ClassName Win32_NetworkAdapter</code></td><td>Network Adapters</td></tr><tr><td><code>Get-WmiObject -Class Win32_NetworkAdapter</code></td><td>Network Adapters</td></tr></tbody></table>

Retrieves basic computer system information about the hardware:

```powershell
wmic computersystem get Manufacturer,Model,SystemType,NumberOfProcessors,TotalPhysicalMemory `| 
```

Get number of processors:

Idle (CPU Time) / smss.exe (Elapsed Time) = CPU Core Count

```powershell
wmic computersystem get numberofprocessors
```

Queries Win32\_Bios:

```powershell
Get-CimInstance -class Win32_BIOS 
```

Same as above but deprecated:

```powershell
Get-WmiObject -Class Win32_BIOS
```

BIOS all information:

```powershell
wmic bios get /format:list
```

## <mark style="color:red;">Registry Locations</mark>

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\HARDWARE\DESCRIPTION\System</mark>

Contains detailed descriptions of system hardware components, including the BIOS, central processor, and system buses.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\HARDWARE\DEVICEMAP</mark>

Provides mappings for hardware devices and their corresponding system resources.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Enum</mark>

Enumerates all devices installed on the system, including detailed information about hardware IDs, driver configurations, and device properties.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services</mark>

Contains information about drivers and services associated with hardware components.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Class</mark>

Includes settings and properties for device classes, such as display adapters, network adapters, and storage controllers.
