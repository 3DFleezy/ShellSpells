# Enumerate

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tasklist /svc</code></mark></td><td>Display running services.</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /svc /fi "imagename eq svchost.exe"</code></mark></td><td>Finds only processes that are svchost.exe and associated services.</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /svc /fi "services eq dnscache"</code></mark></td><td>List Process responsible for a service (DNS Client Service in this case).</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /V /FI "MODULES eq mswsock.dll"</code></mark></td><td>List all process associated with the Windows Socket DLL.</td></tr><tr><td><mark style="color:yellow;"><code>net start</code></mark></td><td>View a list of running services.</td></tr><tr><td><mark style="color:yellow;"><code>net start ^ | find /v /c</code></mark></td><td>Count services.</td></tr><tr><td><mark style="color:yellow;"><code>sc query [ServiceName]</code></mark></td><td>Configuration &#x26; status info.</td></tr><tr><td><mark style="color:yellow;"><code>sc queryex state=all</code></mark></td><td>Shows extended information for all services.</td></tr><tr><td><mark style="color:yellow;"><code>sc enumdepend [ServiceName]</code></mark></td><td>Displays service dependencies.</td></tr><tr><td><mark style="color:yellow;"><code>sc enumdepend tapisrv</code></mark></td><td>List the local services that will not run unless the TAPISRV service is running.</td></tr><tr><td><mark style="color:yellow;"><code>sc enumdepend rpcss 6971</code></mark></td><td>List services that depend on RPCSS service, and specify buffer size of 6,971 bytes.</td></tr><tr><td><mark style="color:yellow;"><code>sc qc lanmanworkstation</code></mark></td><td>View the services the "Workstation" service depends upon.</td></tr><tr><td><mark style="color:yellow;"><code>sc qc w32time</code></mark></td><td>Gets properties of ServiceName. Shows exes.</td></tr><tr><td><mark style="color:yellow;"><code>sc getdisplayname "Scheduler"</code></mark></td><td>Gets DisplayName from the KeyName.</td></tr><tr><td><mark style="color:yellow;"><code>sc getkeyname "Task Scheduler"</code></mark></td><td>Gets KeyName from the DisplayName.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Service</code></mark></td><td>PS - Get service listing.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Service | Where-Object {$_.Status -eq "Stopped"}</code></mark></td><td>Show stopped services.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Service | where Status -eq "Stopped"</code></mark></td><td>Show stopped services.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Service -ComputerName &#x3C;ComputerName></code></mark></td><td>Retrieves the status of services on a specified remote computer.</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance -ClassName Win32_Service</code></mark></td><td>Services.</td></tr><tr><td><mark style="color:yellow;"><code>Get-WmiObject Win32_Service</code></mark></td><td>Retrieves service objects using WMI.</td></tr><tr><td><mark style="color:yellow;"><code>wmic service Name get pathname</code></mark></td><td>Service cmdline.</td></tr><tr><td><mark style="color:yellow;"><code>wmic service list brief</code></mark></td><td>All services with brief details.</td></tr><tr><td><mark style="color:yellow;"><code>wmic service where "state='running'" get name, displayname</code></mark></td><td>Running services with select properties.</td></tr><tr><td><mark style="color:yellow;"><code>wmic service get name,displayname,startmode,pathname</code></mark></td><td>Services and select properties.</td></tr><tr><td><mark style="color:yellow;"><code>service* sc enumdepend lanmanworkstation</code></mark></td><td>View the <em>services that depend upon the "Workstation" service</em>.</td></tr></tbody></table>

Check services for exe:

```powershell
reg query "HKLM\System\CurrentControlSet\Services" /s | find /I "nc.exe"
```



Get all services that the Display Name starts with Windows\*. This is not the actual name of the service. The Display (Human Readable) name.

```powershell
Get-Service -DisplayName 'Windows*' 
```



Allows you to access extended properties such as Description of the service.

```powershell
Get-Service -Name wuauserv | Select-Object -ExpandProperty Description
```



Finds the description of a service "wuauserv" if -ExpandedProperty does not work.

```powershell
Get-CimInstance win32_service | ?{$_.NAME -match "wuauserv"} | select Description 
```



Get cmdline of service or Verbose (/s):

```powershell
reg query "HKLM\System\CurrentControlSet\Services\<Name>" /v "ImagePath"
```

```powershell
reg query "HKLM\System\CurrentControlSet\Services\<Name> /s
```



Query service by name and show the cmdline:

```powershell
$service = get-wmiobject -query 'select * from win32_service where name="Name"'; echo $service.pathname
```



Shows what processes are linked to services:

{% code overflow="wrap" %}
```powershell
get-ciminstance -namespace root/cimv2 -classname Win32_service | select-object displayname,state,processid
```
{% endcode %}

Filter off of service state:

{% code overflow="wrap" %}
```powershell
get-ciminstance -namespace root/cimv2 -classname Win32_service | where-object {$_.state -eq "running"} | select-object displayname,state,processid
```
{% endcode %}



Shows services set to <mark style="color:orange;">bootstart</mark> <mark style="color:orange;">(</mark><mark style="color:orange;">**1**</mark><mark style="color:orange;">)</mark>.

<mark style="color:orange;">**1**</mark> = <mark style="color:orange;">**bootstart**</mark>, these will be unfamiliar services most likely.

<mark style="color:orange;">**2**</mark> = <mark style="color:orange;">**autostart (delayed)**</mark>, which will be services you are more familiar with.

{% code overflow="wrap" %}
```powershell
get-itemproperty HKML:\system\currentcontrolset\services* | where-object {$_.start -eq 1} | select description,imagepath,pschildname | format-list
```
{% endcode %}

This is a good command to run to make sure that services are running the correct processes.

This is how to list DLLs that specific programs are loading. Only works on running programs.

By Name (use the name used in the process list):

{% code overflow="wrap" %}
```powershell
get-process | where-object {$_.name -eq "cmd"} | select-object -ExpandProperty modules | select-object filename
```
{% endcode %}

By Process ID:

{% code overflow="wrap" %}
```powershell
get-process | where-object {$_.id -eq 5648} | select-object -ExpandProperty modules | select-object filename
```
{% endcode %}



## <mark style="color:red;">Remote</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sc \\xp.ops.local query type=service</code></mark></td><td>Remote query</td></tr><tr><td><mark style="color:yellow;"><code>sc \\xp.ops.local getkeyname "Windows Firewall/Internet Connection Sharing (ICS)"</code></mark></td><td>Returns keyname of "sharedaccess"</td></tr><tr><td><mark style="color:yellow;"><code>sc \\xp.ops.local query sharedaccess</code></mark></td><td>Returns Description and Status of the Windows "Security Center" service</td></tr></tbody></table>

Creates 1-to-1 Temporary Session:

```powershell
Invoke-Command -ComputerName File-Server {Get-Service}
```

Running a Temporary Session as a Job:

```powershell
Invoke-Command -ComputerName File-Server,Domain-Controll,Workstation2 {Get-Service} -asjob
```

Running a Temporary Session as a Job:

```powershell
Invoke-Command -ComputerName File-Server,Domain-Controll,Workstation2 {Get-Service} -asjob
```

Displays the job's Results:

```powershell
Receive-Job <job #>
```

\-> don't forget `winrm quickconfig -q` if using PS3+ for PSSession/CIMSession Remote

```powershell
get-ciminstance -classname win32_service -filter "state like 'running'" | select name
```

Create CimSession or PSSession:

```powershell
$c = New-CimSession -ComputerName win10 -Credential barney
```

Get running services on Win10, pipe the CimInstance in:

```powershell
$c | Get-CimInstance -ClassName Win32_Service -filter "State like 'Running'
```

Get service status:

```powershell
Get-CimInstance Win32_Service -Filter "Name='Spooler'" -CimSession $c | Selectlogging Name,State
```

Start service:

```powershell
Get-CimInstance Win32_Service -Filter "Name='Spooler'" -CimSession $c | Invoke-CimMethod -Name StartService
```

### <mark style="color:purple;">Remote For PS3 -> PS2</mark>

```
$dopt = New-CimSessionOption -Protocol Dcom
$d = New-CimSession -ComputerName win7 -Credential fred -SessionOption $dopt
$d | Get-CimInstance -ClassName Win32_Service -filter "State like 'Running'"
```

## <mark style="color:red;">Registry Locations</mark>
