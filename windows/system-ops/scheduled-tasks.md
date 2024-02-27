# Scheduled Tasks

## <mark style="color:red;">Enumerate</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>schtasks</code></mark></td><td>Scheduled tasks</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /query</code></mark></td><td>Scheduled tasks with status</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /query /v</code></mark></td><td>Detailed info</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /query /v list /FO</code></mark></td><td>Scheduled tasks</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /query /v /tn &#x3C;taskname> /fo LIST</code></mark></td><td>Specific task</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /query /s &#x3C;System></code></mark></td><td>Scheduled tasks on specified remote host</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /query /v /FO list | findstr /B "Task Name:" | sort</code></mark></td><td>Find specific task and sort</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /query /fo list /v | findstr /v "\\Microsoft"</code></mark></td><td>Filter out key words like "Microsoft"</td></tr><tr><td><mark style="color:yellow;"><code>Get-ScheduledTask</code></mark></td><td>List all scheduled</td></tr><tr><td><mark style="color:yellow;"><code>Get-ScheduledTask -TaskName &#x3C;TaskName></code></mark></td><td>Specific scheduled task</td></tr><tr><td><mark style="color:yellow;"><code>Get-ScheduledTaskInfo</code></mark></td><td>Last run time and result for all scheduled tasks</td></tr><tr><td><mark style="color:yellow;"><code>Get-ScheduledTaskInfo -TaskName &#x3C;TaskName></code></mark></td><td>Last run time and result for specific scheduled task</td></tr><tr><td><mark style="color:yellow;"><code>Get-ScheduledTask -TaskPath &#x3C;TaskPath></code></mark></td><td>Scheduled tasks in specific folder</td></tr><tr><td><mark style="color:yellow;"><code>Get-ScheduledTask | Where-Object {$_.State -eq 'Running'}</code></mark></td><td>All currently running scheduled tasks</td></tr><tr><td><mark style="color:yellow;"><code>Get-ScheduledTask | ft TaskName,TaskPath,State</code></mark></td><td>All scheduled tasks and only include those three fields</td></tr><tr><td><mark style="color:yellow;"><code>Get-CimInstance -ClassName Win32_ScheduledJob</code></mark></td><td>Retrieves a list of AT-style scheduled jobs (not including tasks created via Task Scheduler)</td></tr></tbody></table>

WMIC:

WMIC is less effective for enumerating modern scheduled tasks and is primarily used for backward compatibility with older systems. Lists AT-style scheduled jobs on the local computer using WMIC:

```powershell
wmic /node:"localhost" /namespace:"\\root\cimv2" path Win32_ScheduledJob get *
```

Filter out keyword "Microsoft\*":

```powershell
Get-ScheduledTask | where {$_.TaskPath -notlike "\\Microsoft\*"} | ft Taskname,TaskPath,State
```

## <mark style="color:red;">Modify</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>schtasks /create /tn &#x3C;TaskName> /tr &#x3C;TaskRun> /sc &#x3C;ScheduleType></code></mark></td><td>Creates a new scheduled task.</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /create /xml &#x3C;XMLFile> /tn &#x3C;TaskName></code></mark></td><td>Creates a new scheduled task from an XML file.</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /change /tn &#x3C;TaskName> [options]</code></mark></td><td>Changes properties of a scheduled task.</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /delete /tn &#x3C;TaskName></code></mark></td><td>Deletes a scheduled task.</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /run /tn &#x3C;TaskName></code></mark></td><td>Runs a scheduled task immediately.</td></tr><tr><td><mark style="color:yellow;"><code>schtasks /end /tn &#x3C;TaskName></code></mark></td><td>Stops a currently running scheduled task.</td></tr><tr><td><mark style="color:yellow;"><code>New-ScheduledTask</code></mark></td><td>Creates a scheduled task definition.</td></tr><tr><td><mark style="color:yellow;"><code>Register-ScheduledTask -TaskName &#x3C;TaskName> -InputObject &#x3C;ScheduledTask></code></mark></td><td>Registers a scheduled task with the Task Scheduler.</td></tr><tr><td><mark style="color:yellow;"><code>Set-ScheduledTask -TaskName &#x3C;TaskName> [options]</code></mark></td><td>Modifies settings of an existing scheduled task.</td></tr><tr><td><mark style="color:yellow;"><code>Unregister-ScheduledTask -TaskName &#x3C;TaskName></code></mark></td><td>Unregisters (deletes) a scheduled task.</td></tr><tr><td><mark style="color:yellow;"><code>Start-ScheduledTask -TaskName &#x3C;TaskName></code></mark></td><td>Starts a scheduled task immediately.</td></tr><tr><td><mark style="color:yellow;"><code>Stop-ScheduledTask -TaskName &#x3C;TaskName></code></mark></td><td>Stops a currently running scheduled task.</td></tr><tr><td><mark style="color:yellow;"><code>Export-ScheduledTask -TaskName &#x3C;TaskName></code></mark></td><td>Exports a scheduled task to an XML file.</td></tr><tr><td><mark style="color:yellow;"><code>Import-ScheduledTask -Xml &#x3C;XMLContent> -TaskName &#x3C;TaskName></code></mark></td><td>Creates a new scheduled task from an XML string or file.</td></tr></tbody></table>

## <mark style="color:red;">Registry Locations</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache</mark>

Contains subkeys with detailed information about scheduled tasks, including:

hierarchical structure of task folders and tasks (Tree)

individual task definitions (Tasks)

tasks scheduled to run at system startup (Boot) or user logon (Logon).

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\CompatibilityAdapter</mark>

Stores information about tasks migrated from older versions of Windows.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\SchedulingAgent</mark>

Used in older versions of Windows, contains information about tasks scheduled using the AT command.
