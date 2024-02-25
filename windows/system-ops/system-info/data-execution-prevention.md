# Data Execution Prevention

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="587">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>wmic OS Get DataExecutionPrevention_Available</code></td><td>Get DEP status</td></tr><tr><td><code>wmic OS get DataExecutionPrevention_Drivers</code></td><td>Determines if DEP is enabled for drivers.</td></tr><tr><td><code>wmic OS get DataExecutionPrevention_SupportPolicy</code></td><td>Retrieves the DEP support policy, indicating how DEP is applied.</td></tr><tr><td><code>systeminfo | find "Data Execution Prevention Available"</code></td><td>Finds DEP availability in the system summary.</td></tr></tbody></table>

Uses PowerShell to get DEP information via WMI:

```powershell
Get-WmiObject Win32_OperatingSystem | Select-Object DataExecutionPrevention_Available, DataExecutionPrevention_Drivers, DataExecutionPrevention_SupportPolicy 
```

## <mark style="color:red;">Registry Locations</mark>

System-wide DEP Configuration:

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management</mark>

The value ExecuteOptions in this key indicates the system-wide DEP configuration.

The data in this value determines how DEP is applied (e.g., for all processes, for essential Windows programs and services only, etc.).



DEP Configuration for Individual Programs:

DEP exceptions for specific programs are not typically stored directly in the registry.

Instead, they are managed through the System Properties interface or command-line tools like bcdedit.

However, information about these settings might be reflected in system configuration files rather than in specific registry keys.
