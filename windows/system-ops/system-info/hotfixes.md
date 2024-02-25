# Hotfixes

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="501">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systeminfo</code></td><td>Extensive system info</td></tr><tr><td><code>Get-HotFix</code></td><td>All installed Microsoft Hotfixes</td></tr><tr><td><code>(get-hotfix).count</code></td><td>Get a count of HotFixes</td></tr><tr><td><code>wmic qfe list</code></td><td>Lists installed Windows hotfixes using WMIC.</td></tr><tr><td><code>wmic qfe get hotfixid</code></td><td>Get a list of HotFixes</td></tr><tr><td><code>dism /online /get-packages</code></td><td>Lists packages, including hotfixes, using DISM.</td></tr><tr><td><code>Get-WmiObject -Class Win32_QuickFixEngineering</code></td><td>Hotfixes via WMI</td></tr></tbody></table>

## <mark style="color:red;">Find Specific Hotfix</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="513">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systeminfo | find "KBxxxxxx"</code></td><td>Specific KB</td></tr><tr><td><code>wmic qfe | find "KB&#x3C;number>"</code></td><td>Specific KB</td></tr><tr><td><code>wmic qfe get HotFixID | find "KBxxxxxx"</code></td><td>Specific KB</td></tr><tr><td><code>regfind -b "KB&#x3C;number>"</code></td><td>Specific KB</td></tr><tr><td><code>Get-HotFix -Id "KBxxxxxx"</code></td><td>Specific KB</td></tr><tr><td><code>dism /online /get-packages | findstr "KBxxxxxx"</code></td><td>Specific KB</td></tr></tbody></table>

PowerShell command to find a hotfix via WMI filtering.

```powershell
Get-WmiObject -query 'select * from win32_quickfixengineering' | foreach {$_.KB<number>}
```

```powershell
Get-WmiObject -Class Win32_QuickFixEngineering | Where-Object {$_.HotFixID -eq "KBxxxxxx"}
```

## <mark style="color:red;">Registry Locations</mark>

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Component Based Servicing\Packages</mark>

This registry key contains information about updates and hotfixes that have been installed by the Component-Based Servicing (CBS).

Each subkey represents a different package or hotfix.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall</mark>

Within this key, there are subkeys for installed programs and updates, including hotfixes.

Hotfixes are typically identified by their KB number (e.g., KBxxxxxxx).

Each subkey contains information about the specific hotfix, such as its display name, installation date, and version.

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall</mark>

On 64-bit versions of Windows, this registry path mirrors the HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall path and contains information about 32-bit programs and updates installed on the system, including 32-bit hotfixes.
