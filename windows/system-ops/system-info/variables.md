# Variables

## <mark style="color:red;">Enumerate</mark>

<table data-header-hidden data-full-width="false"><thead><tr><th width="264">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>Get-Variable</code></td><td>Displays current variables</td></tr><tr><td><code>gci variable:</code></td><td>Same as above</td></tr><tr><td><code>Get-ChildItem env:</code></td><td>List all Environment Variables</td></tr><tr><td><code>set</code></td><td>Lists all environment variables in the Command Prompt.</td></tr><tr><td><code>echo %VARIABLE_NAME%</code></td><td>Shows the value of a specific environment variable in the Command Prompt.</td></tr><tr><td><code>$env:VARIABLE_NAME</code></td><td>Retrieves the value of a specific environment variable in PowerShell.</td></tr><tr><td><code>printenv</code></td><td>Windows Subsystem for Linux (WSL) environment.</td></tr></tbody></table>

## <mark style="color:red;">Modify</mark>

| `Get-Variable`                     | Names are displayed without the preceding <$>                      |
| ---------------------------------- | ------------------------------------------------------------------ |
| `Clear-Variable -Name MyVariable`  | Delete the value of a Variable                                     |
| `Remove-Variable -Name MyVariable` | Delete the Variable                                                |
| `$MyVariable = 1, 2, 3`            | Creates the MyVariable with 1,2,3                                  |
| `$Processes = Get-Process`         | Creates a Variable with the results of Get-Process                 |
| `$Today = (Get-Date).DateTime`     | Creates a combined Date/Time variable from the results of Get-Date |
| `Set-Item -Path Env:/A -Value 1`   | Sets environment variable 'A' to '1'                               |

## Automatic Variables

<table data-header-hidden><thead><tr><th width="205">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>$$</code></td><td>Last token in the last line received by the session.</td></tr><tr><td><code>$?</code></td><td>Execution status of the last operation.</td></tr><tr><td><code>$^</code></td><td>First token in the last line received by the session.</td></tr><tr><td><code>$_</code></td><td>Contains the current object in the pipeline object.</td></tr><tr><td><code>$ARGS</code></td><td>Array of the undeclared parameters and/or parameter values passed to a function, script, or script block.</td></tr><tr><td><code>$ERROR</code></td><td>An array of error objects that represent the most recent errors.</td></tr><tr><td><code>$FALSE</code></td><td>Represent FALSE in commands and scripts instead of using the string "false".</td></tr><tr><td><code>$FOREACH</code></td><td>Enumerator (not the resulting values) of a ForEach loop.</td></tr><tr><td><code>$HOME</code></td><td>Full path of the user’s home directory.</td></tr><tr><td><code>$LASTEXITCODE</code></td><td>Exit code of the last Windows-based program that was run.</td></tr><tr><td><code>$MATCHES</code></td><td>Works with the -match and -notmatch operators.</td></tr><tr><td><code>$NULL</code></td><td>Automatic variable that contains a NULL or empty value.</td></tr><tr><td><code>$PID</code></td><td>Process identifier (PID) of the process hosting the current PowerShell session.</td></tr><tr><td><code>$PROFILE</code></td><td>Full path of the PowerShell profile for the current user and the current host application.</td></tr><tr><td><code>$PSVERSIONTABLE</code></td><td>Read-only hash table displaying details about the version of PowerShell running in the current session.</td></tr><tr><td><code>$TRUE</code></td><td>Used to represent TRUE in commands and scripts.</td></tr></tbody></table>

## <mark style="color:red;">Registry Locations</mark>

Environment variables in Windows are stored in the registry in two primary locations:

System Variables:

<mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment</mark>

This key contains environment variables that are set system-wide and affect all users on the system.

User Variables:

<mark style="color:orange;">HKEY\_CURRENT\_USER\Environment</mark>

This key stores environment variables that are specific to the currently logged-in user.

When you set or modify environment variables via system settings or using tools like <mark style="color:yellow;">`setx`</mark>, the changes are reflected in these registry locations.
