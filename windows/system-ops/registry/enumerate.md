# Enumerate

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>regedit</code></mark></td><td>GUI</td></tr><tr><td><mark style="color:yellow;"><code>reg query HKLM\Software</code></mark></td><td>Lists all subkeys and values</td></tr><tr><td><mark style="color:yellow;"><code>reg query HKCU</code></mark></td><td>Lists subkeys and values under the HKCU registry hive.</td></tr><tr><td><mark style="color:yellow;"><code>reg export HKLM\Software filename.reg</code></mark></td><td>Exports to a .reg file.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ChildItem -Path Registry::HKEY_LOCAL_MACHINE\Software</code></mark></td><td>Enumerates registry keys and values under HKLM in PowerShell.</td></tr><tr><td><mark style="color:yellow;"><code>(Get-Item -Path Registry::HKEY_LOCAL_MACHINE\Software).Property</code></mark></td><td>Lists all value names under a registry key in PowerShell.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\Software</code></mark></td><td>Retrieves properties (values) of the Run key in PowerShell.</td></tr></tbody></table>

## <mark style="color:red;">Basic Query</mark>

Displays values and data for keys under the "Run" key:

```powershell
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

## <mark style="color:red;">Querying a Specific Value</mark>

```powershell
reg query HKCU\Control Panel\Desktop /v Wallpaper
```

Shows the current desktop wallpaper path.

Replace "Wallpaper" with the name of the desired value.

## <mark style="color:red;">Searching for a Value</mark>

```powershell
reg query HKLM /f "Chrome" /t REG_SZ
```

Searches all keys under HKLM (local machine hive) for values containing "Chrome" of type REG\_SZ (string).

## <mark style="color:red;">Searching Recursively</mark>

```powershell
reg query HKLM /s /f "Explorer" /t REG_DWORD
```

Searches all subkeys under HKLM for values containing "Explorer" of type REG\_DWORD (32-bit integer).

## <mark style="color:red;">Comparing Values in Two Keys</mark>

```powershell
reg query HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon /v Shell /ve
```

Displays only empty values for the "Shell" value.

## <mark style="color:red;">Exporting a Key to a File</mark>

```powershell
reg export HKCU\Software\MyApp C:\Backup\MyAppSettings.reg
```

Exports the "MyApp" key and its subkeys to a .reg file for backup or transfer.

## <mark style="color:red;">Remote</mark>

Remote registry: Use \ComputerName\ before the root key to query a remote computer's registry.
