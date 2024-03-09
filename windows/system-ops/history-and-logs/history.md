# History

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="437">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>doshkey /h</code></mark></td><td>Show command history</td></tr><tr><td><mark style="color:yellow;"><code>doskey /history</code></mark></td><td>Displays the command history in the Command Prompt window.</td></tr><tr><td><mark style="color:yellow;"><code>Get-History</code></mark></td><td>Shows the command history of PowerShell sessions.</td></tr><tr><td><mark style="color:yellow;"><code>Clear-History</code></mark></td><td>Clears the command history in the current PowerShell session.</td></tr><tr><td><mark style="color:yellow;"><code>Get-History | Export-Clixml history.xml</code></mark></td><td>Exports PowerShell command history to an XML file named "history.xml."</td></tr><tr><td><mark style="color:yellow;"><code>Import-Clixml history.xml | Add-History</code></mark></td><td>Imports command history from an XML file named "history.xml" and appends it to the current session's history.</td></tr></tbody></table>

Retrieves security event log history using CIM (Common Information Model):

```powershell
Get-CimInstance -ClassName Win32_NTLogEvent -Filter "Logfile='Security'"
```



## <mark style="color:red;">Notes</mark>

<mark style="color:yellow;">`Clear-History`</mark> will clear the history, but leaves this command and the ID (command count).

There is also a file that still has your history located here:

{% code overflow="wrap" fullWidth="true" %}
```powershell
C:\Users\<User>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```
{% endcode %}

To actually clear the history:

1. Run <mark style="color:yellow;">`Clear-History`</mark>
2. Close PowerShell instances.
3. Delete the ConsoleHost\_history.txt file (location above).

