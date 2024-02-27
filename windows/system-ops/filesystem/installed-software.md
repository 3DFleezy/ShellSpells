# Installed Software

## <mark style="color:red;">Enumerate</mark>

Simple Listing:

```powershell
Get-CimInstance -ClassName Win32_Product
```

```powershell
Get-WmiObject -Class Win32_Product | Select-Object Name, Version
```

```powershell
Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall* | Select-Object DisplayName, DisplayVersion, Publisher | Format-Table –AutoSize
```

More Details:

```powershell
Get-WmiObject -Class Win32_Product | Select-Object Name, Version, InstallDate, Vendor
```

```powershell
wmic /output:C:\InstalledSoftware.txt product get name, version, description, installdate, vendor
```

Export to File:

```powershell
Get-WmiObject -Class Win32_Product | Select-Object Name, Version, InstallDate, Vendor | Export-Csv -Path "C:\InstalledSoftware.csv" -NoTypeInformation
```

## <mark style="color:red;">Install / Uninstall</mark>

### <mark style="color:purple;">Executable (.exe) Installers</mark>

| <mark style="color:yellow;">`<InstallerName>.exe`</mark>           | Runs an executable installer with its default configuration.                                      |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------- |
| <mark style="color:yellow;">`<InstallerName>.exe /?`</mark>        | Displays available command-line options for the executable installer.                             |
| <mark style="color:yellow;">`<InstallerName>.exe /silent`</mark>   | Installs the software silently without user interaction (specific options vary by installer).     |
| <mark style="color:yellow;">`<UninstallerName>.exe`</mark>         | Runs an executable uninstaller with its default configuration.                                    |
| <mark style="color:yellow;">`<UninstallerName>.exe /?`</mark>      | Displays available command-line options for the executable uninstaller.                           |
| <mark style="color:yellow;">`<UninstallerName>.exe /silent`</mark> | Uninstalls the software silently without user interaction (specific options vary by uninstaller). |

### <mark style="color:purple;">Windows Installer (.msi) Packages</mark>

| <mark style="color:yellow;">`msiexec /i <PackageName>.msi`</mark>     | Installs an MSI package.                                  |
| --------------------------------------------------------------------- | --------------------------------------------------------- |
| <mark style="color:yellow;">`msiexec /i <PackageName>.msi /qn`</mark> | Installs an MSI package quietly without user interface.   |
| <mark style="color:yellow;">`msiexec /x <PackageName>.msi`</mark>     | Uninstalls an MSI package.                                |
| <mark style="color:yellow;">`msiexec /x <PackageName>.msi /qn`</mark> | Uninstalls an MSI package quietly without user interface. |
| <mark style="color:yellow;">`msiexec /x {<ProductCode>}`</mark>       | Uninstalls an MSI package using its product code.         |

Installs an MSI package with a transform file to customize the installation.

```powershell
msiexec /i <PackageName>.msi TRANSFORMS=<TransformFile>.mst
```

### <mark style="color:purple;">PowerShell</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Install-Package -Name &#x3C;PackageName></code></mark></td><td>Installs a package from a package provider</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process -FilePath &#x3C;InstallerName>.exe -ArgumentList '/silent'</code></mark></td><td>Runs an executable installer quietly.</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process -FilePath msiexec -ArgumentList '/i &#x3C;PackageName>.msi /qn'</code></mark></td><td>Installs an MSI package quietly.</td></tr><tr><td><mark style="color:yellow;"><code>Uninstall-Package -Name &#x3C;PackageName></code></mark></td><td>Uninstalls a package from a package</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process -FilePath &#x3C;UninstallerName>.exe -ArgumentList '/silent'</code></mark></td><td>Runs an executable uninstaller quietly.</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process -FilePath msiexec -ArgumentList '/x &#x3C;PackageName>.msi /qn'</code></mark></td><td>Uninstalls an MSI package quietly.</td></tr></tbody></table>

### <mark style="color:purple;">Windows Package Manager (winget)</mark>

| <mark style="color:yellow;">`winget install <PackageName>`</mark>   | Installs package   |
| ------------------------------------------------------------------- | ------------------ |
| <mark style="color:yellow;">`winget uninstall <PackageName>`</mark> | Uninstalls package |

### Uninstall applications that begin with Google

```powershell
(Get-WmiObject Win32_Product -computername win7 -credential fred -filter "Name like '%Google%'").Uninstall()
```
