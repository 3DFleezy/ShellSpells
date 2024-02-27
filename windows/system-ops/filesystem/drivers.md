# Drivers

## <mark style="color:red;">Enumerate</mark>

| <mark style="color:yellow;">`lm`</mark>                                  | Displays loaded kernel modules (aka Drivers).                       |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| <mark style="color:yellow;">`driverquery /v`</mark>                      | Lists driver information in verbose mode.                           |
| <mark style="color:yellow;">`driverquery`</mark>                         | Lists all installed drivers and their properties.                   |
| <mark style="color:yellow;">`Get-WmiObject Win32_PnPSignedDriver`</mark> | PowerShell command to get detailed driver information.              |
| <mark style="color:yellow;">`pnputil /enum-drivers`</mark>               | Enumerates all drivers in the driver store.                         |
| <mark style="color:yellow;">`dism /online /get-drivers`</mark>           | Lists drivers using Deployment Image Servicing and Management tool. |

WMIC:

```powershell
wmic sysdriver get displayname,pathname,started,status
```

## <mark style="color:red;">Registry Locations</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services</mark>

This key contains subkeys for each service and driver installed on the system. Each subkey includes information about the driver's configuration, type, start type, and path to the executable.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Drivers32</mark>

Stores information about 32-bit drivers, particularly for multimedia components like audio and video drivers.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Setup\PnpResources\Registry\HKLM\SYSTEM\CurrentControlSet\Control\Class</mark>

Contains settings for all hardware device classes. Each class GUID subkey holds information about the drivers associated with that class of devices.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Class</mark>

This key is similar to the one above and contains a list of all device classes with their corresponding settings and installed drivers.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Enum</mark>

This key enumerates all hardware devices and their driver information. It includes details such as device IDs, driver versions, and hardware capabilities.

## <mark style="color:red;">Notes</mark>

In the context of Windows operating systems, kernel modules are essentially the same as drivers. In Windows, drivers are a specific type of kernel module. The term "kernel module" generally refers to a software component that can be loaded into the kernel of an operating system to extend its capabilities or provide support for hardware devices.

In Windows, these kernel modules are typically called drivers, especially when they are used to enable the operating system to interact with hardware devices, such as graphics cards, network adapters, and storage devices. Drivers operate at the kernel level, allowing the operating system to communicate with and control hardware.

While the term "kernel module" is more commonly used in Unix-like operating systems (e.g., Linux), the concept is similar in Windows. Drivers in Windows can be:

Device Drivers: Software that allows the operating system to communicate with hardware or virtual devices. System Drivers: Software components that provide core functionality within the operating system, such as file system drivers.
