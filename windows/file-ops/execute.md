# Execute

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="537">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>C:\path\to\yourscript.bat</code></mark></td><td>Executes a batch script located at the specified path using CMD.</td></tr><tr><td><mark style="color:yellow;"><code>powershell -File C:\path\to\yourscript.ps1</code></mark></td><td>Executes a PowerShell script (.ps1 file) from CMD.</td></tr><tr><td><mark style="color:yellow;"><code>start C:\path\to\yourprogram.exe</code></mark></td><td>CMD to run an executable program.</td></tr><tr><td><mark style="color:yellow;"><code>&#x26; "C:\path\to\yourscript.ps1"</code></mark></td><td>Executes a PowerShell script from within a PowerShell session.</td></tr><tr><td><mark style="color:yellow;"><code>&#x26; "C:\path\to\yourprogram.exe"</code></mark></td><td>Directly executes an executable program from a PowerShell session.</td></tr><tr><td><mark style="color:yellow;"><code>.\yourscript.ps1</code></mark></td><td>Runs a PowerShell script located in the current directory from a PowerShell session.</td></tr><tr><td><mark style="color:yellow;"><code>Invoke-Expression -Command "C:\path\to\yourscript.ps1"</code></mark></td><td>Executes a PowerShell script using <code>Invoke-Expression</code>in PowerShell.</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process -FilePath "C:\path\to\yourprogram.exe"</code></mark></td><td>Starts an executable program from PowerShell.</td></tr><tr><td><mark style="color:yellow;"><code>cmd /c C:\path\to\yourscript.bat</code></mark></td><td>Executes a batch script from within a PowerShell session using CMD.</td></tr></tbody></table>

Starts a PowerShell script using `Start-Process` in PowerShell.

```powershell
Start-Process -FilePath "powershell.exe" -ArgumentList "-File C:\path\to\yourscript.ps1"
```

## <mark style="color:red;">Command Prompt (CMD)</mark>

Execute a script:

script\_name.bat for batch files (.bat)

script\_name.cmd for command files (.cmd)

script\_name.vbs for Visual Basic scripts (.vbs)

script\_name.ps1 for PowerShell scripts (.ps1), requires enabling script execution first

Execute an executable: <mark style="color:yellow;">`executable_name.exe`</mark>

## <mark style="color:red;">PowerShell</mark>

Execute a script:

```powershell
.\script_name.ps1
```

```powershell
& 'C:\path\to\script.ps1'
```

Execute an executable:

```powershell
Start-Process executable_name.exe
```
