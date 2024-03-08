# Enumerate

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tasklist /startup</code></mark></td><td>Lists all auto-start processes registered on the system.</td></tr><tr><td><mark style="color:yellow;"><code>wmic startup list full</code></mark></td><td>Lists detailed information about auto-start entries using WMIC.</td></tr><tr><td><mark style="color:yellow;"><code>wmic startup get caption,command</code></mark></td><td>View Startup Processes.</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance Win32_StartupCommand</code></mark></td><td>Retrieves auto-start commands using CIM.</td></tr><tr><td><mark style="color:yellow;"><code>Get-WmiObject Win32_Service | Where-Object {$_.StartMode -eq "Auto"}</code></mark></td><td>Lists services set to start automatically.</td></tr><tr><td><mark style="color:yellow;"><code>wmic service list brief | findstr /i "auto"</code></mark></td><td>Lists services set to start automatically using WMIC.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run'</code></mark></td><td>Lists registry entries for auto-start programs in HKLM.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ItemProperty -Path 'HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run'</code></mark></td><td>Lists registry entries for auto-start programs in HKCU.</td></tr></tbody></table>

## <mark style="color:red;">Sysinternals</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="285">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>autorunsc -a b</code></mark></td><td>Shows files with attribute "BootExecute". Only Microsoft processes should be running at boot.</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -a t</code></mark></td><td>Shows tasks set to run at startup.</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -m</code></mark></td><td>Filters out software that says it is Microsoft</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -m -s</code></mark></td><td>Filters out software signed by Microsoft</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -s</code></mark></td><td>Services</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -t</code></mark></td><td>Tasks</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -b</code></mark></td><td>Boot execute</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -d</code></mark></td><td>App init DLLs</td></tr></tbody></table>

## <mark style="color:red;">File Locations</mark>

**Individual User Startup (Win10):**&#x20;

```powershell
"C:\Users<user>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup"
```

**Old Individual User Startup:**&#x20;

```powershell
"C:\Documents & Settings\%userprofile%\Start Menu\Programs\Startup"
```

**All Users Startup (Win10):**

```powershell
"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"
```

**Old All Users Startup:**

```powershell
"C:\Documents & Settings\All Users\StartMenu\Programs\StartUp"
```

