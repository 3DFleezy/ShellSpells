# Modify

## <mark style="color:red;">Processes</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>start &#x3C;ProgramName></code></mark></td><td>Starts a program or command in a new window.</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process Notepad.exe</code></mark></td><td>Uses Process.Start Method of the System.Diagnostics.Process class</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process &#x3C;FilePath></code></mark></td><td>Starts one or more processes on the local computer.</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process &#x3C;FilePath> -ArgumentList &#x3C;Arguments></code></mark></td><td>Starts a process with arguments.</td></tr><tr><td><mark style="color:yellow;"><code>Start-Process &#x3C;FilePath> -Verb RunAs</code></mark></td><td>Starts a process with elevated permissions (as administrator).</td></tr><tr><td><mark style="color:yellow;"><code>Start-Job {Start-Process &#x3C;FilePath>}</code></mark></td><td>Starts a process in a background job.</td></tr><tr><td><mark style="color:yellow;"><code>(Get-Process calculator*).kill()</code></mark></td><td>Uses the kill() method directly</td></tr><tr><td><mark style="color:yellow;"><code>Stop-Process -name calculator*</code></mark></td><td>Cmdlet calls the Process.Kill method</td></tr><tr><td><mark style="color:yellow;"><code>Stop-Process -name notepad</code></mark></td><td>Uses Process.Kill Method of the System.Diagnostics.Process class</td></tr><tr><td><mark style="color:yellow;"><code>Stop-Process -Id &#x3C;ProcessID></code></mark></td><td>Stops (ends) the process with the specified process ID.</td></tr><tr><td><mark style="color:yellow;"><code>taskkill /IM &#x3C;ProcessName></code></mark></td><td>Kill by name</td></tr><tr><td><mark style="color:yellow;"><code>taskkill /PID &#x3C;ProcessID></code></mark></td><td>Kill by PID</td></tr><tr><td><mark style="color:yellow;"><code>taskkill /T /IM &#x3C;ProcessName></code></mark></td><td>Kill process and child processes</td></tr><tr><td><mark style="color:yellow;"><code>taskkill /F /IM &#x3C;ProcessName></code></mark></td><td>Force Kill by name</td></tr><tr><td><mark style="color:yellow;"><code>taskkill /F /PID &#x3C;ProcessID></code></mark></td><td>Force Kill by PID</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where name="&#x3C;ProcessName>" delete</code></mark></td><td>Terminates a process with the specified name.</td></tr><tr><td><mark style="color:yellow;"><code>wmic process where processid="&#x3C;ProcessID>" delete</code></mark></td><td>Terminates a process with the specified process ID.</td></tr><tr><td><mark style="color:yellow;"><code>wmic process call create "&#x3C;Command>"</code></mark></td><td>Creates (starts) a process running a specified command.</td></tr></tbody></table>

Run as the user creds you supply:

```powershell
runas /password /user:<username> C:\sus.exe 
```

Quietly start your malicious installer:

```powershell
msiexec /quiet /qn /i C:\sus.msi
```

## <mark style="color:red;">DLLs</mark>

Registers a DLL file with the system.

This command is used to register a DLL file with the system.

When a DLL is registered, the information about its classes and interfaces is added to the Windows Registry, allowing COM clients to use the DLL.

WARNING: May execute code if the DLL has a DllRegisterServer entry point:

```powershell
regsvr32 <DLLName>
```

Unregisters a DLL file from the system. This command unregisters a DLL file from the system, removing its class and interface information from the Windows Registry:

```powershell
regsvr32 /u <DLLName>
```

Executes a function located in a specified DLL. Typically used for DLLs that expose functions compatible with the rundll32 requirements:

```powershell
rundll32.exe <DLLName>,<EntryPoint>
```

Uses PowerShell to load a DLL and execute a specific method:

{% code overflow="wrap" %}
```powershell
PowerShell -Command "[System.Reflection.Assembly]::LoadFile('<FullPathToDLL>').GetType('<Namespace.ClassName>').GetMethod('<MethodName>').Invoke($null, $null)"
```
{% endcode %}

## <mark style="color:red;">Registry Locations</mark>

### <mark style="color:purple;">Processes</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run</mark>

Contains entries for programs and processes that are launched automatically at startup for all users.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Run</mark>

Contains entries for programs and processes that are launched automatically at startup for the current user.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce</mark>

Contains entries for programs and processes that are run once and then removed the next time the system starts.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce</mark>

Contains entries for programs and processes that are run once for the current user and then removed the next time the user logs in.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options</mark>

Contains options and settings for debugging and customizing the execution of specific executable files, including processes.

### <mark style="color:purple;">DLLs</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\SharedDLLs</mark>

Contains paths and reference counts for shared DLLs used by multiple applications.

<mark style="color:blue;">HKEY\_CLASSES\_ROOT\CLSID{CLSID}\InprocServer32</mark>

Contains registration information for COM DLLs, including the path to the DLL file and threading model for each class identified by its CLSID.

<mark style="color:blue;">HKEY\_CLASSES\_ROOT\TypeLib{TypeLibID}</mark>

Contains information about the type libraries, which may include DLLs, registered on the system.

Each type library is identified by a unique ID.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows\AppInit\_DLLs</mark>

Contains names of DLLs to be loaded into every process that uses User32.dll.

This feature is often used by software for customization or extension purposes, but it can also be abused by malware.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\KnownDLLs</mark>

Lists the names of DLLs that are known to the system and are loaded from a trusted location, typically used to improve performance and security.
