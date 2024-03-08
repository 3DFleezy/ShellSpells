# Enumerate

## <mark style="color:red;">Process List</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tasklist</code></mark></td><td>Displays a list of currently running processes on the local computer.</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /FO [table OR list OR csv]</code></mark></td><td>Format Process List</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /s &#x3C;servername></code></mark></td><td>Displays processes running on a remote computer.</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /v</code></mark></td><td>Displays detailed information about processes, including the username of the process owner.</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /m</code></mark></td><td>Displays all processes and the modules loaded by each process.</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /FI "[FilterName] [Operator] [Value]"</code></mark></td><td>Filter Process List</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process</code></mark></td><td>Process list (local or remote)</td></tr><tr><td><mark style="color:yellow;"><code>(GetProcess).Name</code></mark></td><td>Returns only names of every process</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process -Name &#x3C;processname></code></mark></td><td>Gets a process with a specific name.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process -Id &#x3C;processid></code></mark></td><td>Gets a process with a specific process ID.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process -ComputerName &#x3C;computername></code></mark></td><td>Gets processes running on a specified remote computer.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process | where Handles -GE 1000</code></mark></td><td>Process with 1000 or more handles</td></tr><tr><td><mark style="color:yellow;"><code>wmic process get /?</code></mark></td><td>All available fields</td></tr><tr><td><mark style="color:yellow;"><code>wmic process list</code></mark></td><td>Process list</td></tr><tr><td><mark style="color:yellow;"><code>wmic process list brief</code></mark></td><td>Lists all processes with brief details.</td></tr><tr><td><mark style="color:yellow;"><code>wmic process get name,processid</code></mark></td><td>Lists all processes with their names and process IDs.</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where "name='processname.exe'" get *</code></mark></td><td>Retrieves detailed information about a specific process.</td></tr><tr><td><mark style="color:yellow;"><code>wmic process get name,commandline</code></mark></td><td>Command line for each process</td></tr><tr><td><mark style="color:yellow;"><code>wmic process get name,creationdate</code></mark></td><td>Process creation time</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance Win32_Process</code></mark></td><td>Retrieves a list of processes using CIM.</td></tr></tbody></table>



Shows pertinent process info:

{% code overflow="wrap" %}
```powershell
get-ciminstance win32_process | select-object name,processID,parentprocessID,exeutablepath,commandline | format-table
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
gcim win32_process | select name,processID,parentprocessID,executablepath,commandline | ft
```
{% endcode %}

Retrieves detailed information about a specific process using CIM:

```powershell
Get-CimInstance Win32_Process -Filter "name = 'processname.exe'"
```

Processes that have > 1000 Handles:

```powershell
Get-Process | Where-Object -Property Handles -GE -Value 1000 
```

Retrieves the specific properties for every process in list format:

{% code overflow="wrap" %}
```powershell
wmic process get Name,Commandline,ExecutablePath,HandleCount,Priority,ThreadCount /format:list
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
wmic process get name,ProcessID,ParentProcessID,ExecutablePath,CommandLine /FORMAT:LIST
```
{% endcode %}

Show Process Path:

```powershell
wmi win32_process | select Handle, CommandLine | format-list
```

```powershell
wmi win32_process | select name
```

```powershell
wmi win32_process | select CommandLine
```

{% code overflow="wrap" %}
```powershell
wmic process get name,ProcessID,ParentProcessID,ExecutablePath,CommandLine /FORMAT:LIST
```
{% endcode %}

Remote:

{% code overflow="wrap" %}
```powershell
wmic /node:xp /user:xp\administrator /password:L33tHax0r process get name,ProcessID,ParentProcessID,ExecutablePath,CommandLine /FORMAT:LIST
```
{% endcode %}

```powershell
tasklist /S xp /U xp\administrator /P L33tHax0r
```

## <mark style="color:red;">Specific Processes</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tasklist /FI "IMAGENAME eq explorer.exe" /V</code></mark></td><td>Verbose process info</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /V /FI "MODULES eq mswsock.dll"</code></mark></td><td>Process associated with a DLL</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /FI "IMAGENAME eq cmd.exe" /M</code></mark></td><td>DLLs associated with a process</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /svc /fi "services eq dnscache"</code></mark></td><td>List Process responsible for a service</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where processid="772" list brief</code></mark></td><td>PID</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where processid="772" list full</code></mark></td><td>PID</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where (processid=2000) get parentprocessid</code></mark></td><td>PID get PPID</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where (processid=1644) get commandline</code></mark></td><td>PID get cmdline</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where "name like '%.exe" call getowner</code></mark></td><td>Get list of *.exe process owners</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where name="explorer.exe" call getowner</code></mark></td><td>Get ownder of process</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where name='alg.exe' get executablepath,commandline</code></mark></td><td>Process properties</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where name='nc.exe' get installdate</code></mark></td><td>Process properties</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where name='apnmcp.exe' get executablepath</code></mark></td><td>Process properties</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where "caption like 'cmd.exe'" get /format:list</code></mark></td><td>All process properties listed for exe</td></tr><tr><td><mark style="color:yellow;"><code>wmic datafile where name='c:\\\\pathto\\\\exe'</code></mark></td><td>View file properties on a process</td></tr><tr><td><mark style="color:yellow;"><code>wmic datafile where name='c:\\pathto\\exe' get</code></mark></td><td>Get info on unknown process.</td></tr></tbody></table>

```powershell
wmic datafile where name='c:\\pathto\\exe' list full /format:list
```

```powershell
wmic datafile where name='c:\\pathto\\exe' get creationdate, installdate, lastmodified
```

Show process properties:

```powershell
wmic datafile where name='c:\\\\pathto\\\\exe' get creationdate,installdate
```

```powershell
wmic process where "name='vmtoolsd.exe'" get ProcessID,ParentProcessID,ExecutablePath,CommandLine /FORMAT:LIST
```

```powershell
wmic process where "name='mysqld.exe'" get ProcessID, ExecutablePath /FORMAT:LIST
```

Show Process Paths:

```powershell
wmic process where "name='mysqld.exe'" get ProcessID, ExecutablePath
```

```powershell
wmic process where "name='mysqld.exe'" get ProcessID, ExecutablePath /FORMAT:LIST
```

```powershell
wmic process where "name='vmtoolsd.exe'" get ProcessID,ParentProcessID,ExecutablePath,CommandLine /FORMAT:LIST
```

```powershell
wmic datafile where name='c:\\pathto\\exe' get creationdate,installdate
```

## <mark style="color:red;">DLLs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tasklist /M</code></mark></td><td>List the DLLs associated with each process</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /FI "IMAGENAME eq cmd.exe" /M</code></mark></td><td>Lists all DLLs for a process</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /m /FI "modules eq mpr.dll" | more</code></mark></td><td>Lists all DLLs for a process</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /V /FI "MODULES eq mswsock.dll"</code></mark></td><td>List all process associated with the Windows Socket DLL</td></tr><tr><td><mark style="color:yellow;"><code>listdlls -d msctf.dll -accepteula | more</code></mark></td><td>Sysinternals</td></tr></tbody></table>

Check for AppInit\_DLL's (possible rootkit):

```powershell
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Windows"
```

## <mark style="color:red;">SysInternals</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>listdlls -accepteula | find "Command"</code></mark></td><td>Lists all DLLs being used</td></tr><tr><td><mark style="color:yellow;"><code>listdlls -accepteula | find /I "Command"</code></mark></td><td></td></tr><tr><td><mark style="color:yellow;"><code>listdlls -accepteula &#x3C;processname</code></mark></td><td>Lists DLLs of a process</td></tr><tr><td><mark style="color:yellow;"><code>pslist</code></mark></td><td>Tasklist alternative, sysinternals (use -x, -t)</td></tr><tr><td><mark style="color:yellow;"><code>pslist -t</code></mark></td><td>Find parent processes</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -s | find /I "nc.exe"</code></mark></td><td>Checks autostart services and non-disabled drivers</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -w | find /I "nc.exe"</code></mark></td><td>Checks winlogon entries</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -l | find /I "nc.exe"</code></mark></td><td>Checks logon startups (default)</td></tr><tr><td><mark style="color:yellow;"><code>autorunsc -> autodump.txt</code></mark></td><td>Output to txt</td></tr><tr><td><mark style="color:yellow;"><code>more autodump.txt | find /N /I "nc.exe"</code></mark></td><td>Search contents</td></tr><tr><td><mark style="color:yellow;"><code>more /E autodump.txt</code></mark></td><td>Press "=" to show line numbers</td></tr><tr><td><mark style="color:yellow;"><code>accesschk.exe /accepteula -uwcqv &#x3C;user> &#x3C;service></code></mark></td><td>Show permissions on a service/exe</td></tr></tbody></table>
