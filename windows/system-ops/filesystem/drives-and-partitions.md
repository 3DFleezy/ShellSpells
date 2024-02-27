# Drives & Partitions

## <mark style="color:red;">Enumerate</mark>

| <mark style="color:yellow;">`wmic logicaldisk get name`</mark> | Lists all drives using WMIC.             |
| -------------------------------------------------------------- | ---------------------------------------- |
| <mark style="color:yellow;">`fsutil fsinfo drives`</mark>      | Displays drives using FSUtil utility.    |
| <mark style="color:yellow;">`Get-PSDrive`</mark>               | Lists drives in PowerShell.              |
| <mark style="color:yellow;">`net use`</mark>                   | Shows network-mapped drives.             |
| <mark style="color:yellow;">`bcdedit /enum all`</mark>         | Lists drives in boot configuration data. |

View Drives on machine (includes mapped drives):

```powershell
Get-WmiObject -Class Win32_LogicalDisk
```

```powershell
Get-WmiObject -Class Win32_LogicalDisk -Filter “DriveType=3”
```

## <mark style="color:red;">Modify</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>format &#x3C;DriveLetter>: /FS:&#x3C;FileSystem></code></mark></td><td>Formats a drive with the specified file system (e.g., NTFS, FAT32).</td></tr><tr><td><mark style="color:yellow;"><code>label &#x3C;DriveLetter>: &#x3C;NewLabel></code></mark></td><td>Assigns a new label to a drive.</td></tr><tr><td><mark style="color:yellow;"><code>subst &#x3C;DriveLetter>: &#x3C;Path></code></mark></td><td>Creates a virtual drive that is mapped to a specified folder path.</td></tr><tr><td><mark style="color:yellow;"><code>subst &#x3C;DriveLetter>: /D</code></mark></td><td>Deletes a previously created virtual drive.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Disk</code></mark></td><td>Retrieves disk information.</td></tr><tr><td><mark style="color:yellow;"><code>Initialize-Disk -Number &#x3C;DiskNumber></code></mark></td><td>Initializes a disk, preparing it for use.</td></tr><tr><td><mark style="color:yellow;"><code>New-Partition -DiskNumber &#x3C;DiskNumber> -UseMaximumSize -AssignDriveLetter</code></mark></td><td>Creates a new partition on a disk and assigns a drive letter.</td></tr><tr><td><mark style="color:yellow;"><code>Format-Volume -DriveLetter &#x3C;DriveLetter> -FileSystem &#x3C;FileSystem></code></mark></td><td>Formats a volume with the specified file system.</td></tr><tr><td><mark style="color:yellow;"><code>Set-Partition -DriveLetter &#x3C;DriveLetter> -NewDriveLetter &#x3C;NewDriveLetter></code></mark></td><td>Changes the drive letter of a partition.</td></tr><tr><td><mark style="color:yellow;"><code>Remove-Partition -DriveLetter &#x3C;DriveLetter></code></mark></td><td>Removes a partition from a disk.</td></tr></tbody></table>

### <mark style="color:red;">DiskPart Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>diskpart</code></mark></td><td>Launches the DiskPart command-line tool for disk management tasks.</td></tr><tr><td><mark style="color:yellow;"><code>list disk</code></mark></td><td>Displays a list of disks.</td></tr><tr><td><mark style="color:yellow;"><code>select disk &#x3C;DiskNumber></code></mark></td><td>Selects a disk for subsequent operations.</td></tr><tr><td><mark style="color:yellow;"><code>clean</code></mark></td><td>Removes all partitions and data from the selected disk.</td></tr><tr><td><mark style="color:yellow;"><code>create partition primary</code></mark></td><td>Creates a primary partition on the selected disk.</td></tr><tr><td><mark style="color:yellow;"><code>format fs=&#x3C;FileSystem> quick</code></mark></td><td>Formats the selected partition with the specified file system.</td></tr><tr><td><mark style="color:yellow;"><code>assign letter=&#x3C;DriveLetter></code></mark></td><td>Assigns a drive letter to the selected partition.</td></tr><tr><td><mark style="color:yellow;"><code>remove letter=&#x3C;DriveLetter></code></mark></td><td>Removes the drive letter from the selected partition.</td></tr></tbody></table>

## <mark style="color:red;">Registry Locations</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem</mark>

Contains settings and configurations related to the filesystem, including NTFS-specific settings, file system performance tweaks, and other file system behavior settings.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Shares</mark>

Stores information about shared folders on the system, including the path, share name, and share properties.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList</mark>

Contains information about user profiles on the system, including the location of user-specific directories and files.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\VolumeCaches</mark>

Contains settings for disk cleanup of various types of files and data stored on the filesystem.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\Ntfs</mark>

Contains settings specific to the NTFS file system, such as performance optimizations and security settings.
