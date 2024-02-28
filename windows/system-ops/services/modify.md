# Modify

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>net start &#x3C;service></code></mark></td><td>Start Service</td></tr><tr><td><mark style="color:yellow;"><code>net pause</code></mark></td><td>Pause service</td></tr><tr><td><mark style="color:yellow;"><code>net continue</code></mark></td><td>Continue service</td></tr><tr><td><mark style="color:yellow;"><code>net stop &#x3C;service></code></mark></td><td>Stop Service</td></tr><tr><td><mark style="color:yellow;"><code>sc create &#x3C;ServiceName> binPath= "&#x3C;PathToExecutable>"</code></mark></td><td>Creates a new service.</td></tr><tr><td><mark style="color:yellow;"><code>sc delete &#x3C;ServiceName></code></mark></td><td>Deletes a service.</td></tr><tr><td><mark style="color:yellow;"><code>sc start &#x3C;service></code></mark></td><td>Start Service</td></tr><tr><td><mark style="color:yellow;"><code>sc pause &#x3C;ServiceName></code></mark></td><td>Pauses a service.</td></tr><tr><td><mark style="color:yellow;"><code>sc continue &#x3C;ServiceName></code></mark></td><td>Resumes a paused service.</td></tr><tr><td><mark style="color:yellow;"><code>sc stop &#x3C;service></code></mark></td><td>Stop Service</td></tr><tr><td><mark style="color:yellow;"><code>sc config [ServiceName] [Options]</code></mark></td><td>Configure Service</td></tr><tr><td><mark style="color:yellow;"><code>sc config &#x3C;ServiceName> start= &#x3C;startType></code></mark></td><td>Changes the startup type of a service.</td></tr><tr><td><mark style="color:yellow;"><code>sc config wzcsvc start=demand</code></mark></td><td>Sets Wireless Service to Manual</td></tr><tr><td><mark style="color:yellow;"><code>sc config WZCSVC start=disable</code></mark></td><td>Sets Wireless Service to Disabled</td></tr><tr><td><mark style="color:yellow;"><code>sc config netlogon start=disabled</code></mark></td><td>Config netlogon</td></tr></tbody></table>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>New-Service -Name &#x3C;ServiceName> -BinaryPathName "&#x3C;PathToExecutable>"</code></mark></td><td>Creates a new service.</td></tr><tr><td><mark style="color:yellow;"><code>Remove-Service -Name &#x3C;ServiceName></code></mark></td><td>Deletes a service (PowerShell 6+).</td></tr><tr><td><mark style="color:yellow;"><code>Set-Service -Name &#x3C;ServiceName> -StartupType &#x3C;StartType></code></mark></td><td>Changes the startup type of a service.</td></tr><tr><td><mark style="color:yellow;"><code>Start-Service -Name &#x3C;ServiceName></code></mark></td><td>Starts a service.</td></tr><tr><td><mark style="color:yellow;"><code>Stop-Service -Name &#x3C;ServiceName></code></mark></td><td>Stops a service.</td></tr><tr><td><mark style="color:yellow;"><code>Suspend-Service -Name &#x3C;ServiceName></code></mark></td><td>Suspends a service.</td></tr><tr><td><mark style="color:yellow;"><code>Resume-Service -Name &#x3C;ServiceName></code></mark></td><td>Resumes a suspended service.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Service -Name &#x3C;ServiceName></code></mark></td><td>Retrieves the current status of a specific service.</td></tr></tbody></table>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>wmic service where name="&#x3C;ServiceName>" call change startmode="&#x3C;StartMode>"</code></mark></td><td>Changes the startup type of a service.</td></tr><tr><td><mark style="color:yellow;"><code>wmic service where name="&#x3C;ServiceName>" call startservice</code></mark></td><td>Starts a service.</td></tr><tr><td><mark style="color:yellow;"><code>wmic service where name="&#x3C;ServiceName>" call stopservice</code></mark></td><td>Stops a service.</td></tr></tbody></table>

Sets the binary that executes when the service runs:

```powershell
sc config <serviceName> binpath="\\"C:\\PrivEsc\\reverse.exe\\""
```

## <mark style="color:red;">Service Name vs Display (key) Name</mark>

* SERVICE\_NAME = Winmgmt
* DISPLAY\_NAME = Windows Management Instrumentation <--also called keyname