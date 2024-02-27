# Logs

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>eventvwr</code></mark></td><td>Opens the Event Viewer (GUI).</td></tr><tr><td><mark style="color:yellow;"><code>wevtutil qe &#x3C;LogName></code></mark></td><td>Retrieves events from a specific event log.</td></tr><tr><td><mark style="color:yellow;"><code>Get-EventLog -LogName &#x3C;LogName></code></mark></td><td>View specified event logs.</td></tr><tr><td><mark style="color:yellow;"><code>Get-WinEvent -LogName &#x3C;LogName></code></mark></td><td>View specified event logs.</td></tr><tr><td><mark style="color:yellow;"><code>Get-WmiObject -Class Win32_NTLogEvent</code></mark></td><td>View specified event logs using WMI.</td></tr><tr><td><mark style="color:yellow;"><code>logman query</code></mark></td><td>Lists the configured performance counter and event trace logs.</td></tr><tr><td><mark style="color:yellow;"><code>tracerpt &#x3C;LogFileName></code></mark></td><td>Converts event trace logs or performance counter logs into a readable format.</td></tr><tr><td><mark style="color:yellow;"><code>type &#x3C;LogFileName></code></mark></td><td>Displays the contents of a text-based log file.</td></tr></tbody></table>

View specified event logs using WMI and a custom query:

```powershell
Get-WmiObject -Query "SELECT * FROM Win32_NTLogEvent WHERE Logfile = '<LogName>'"
```

View specified event logs using CIM:

```powershell
Get-CimInstance -ClassName Win32_NTLogEvent
```

View specified event logs using CIM and a custom query:

{% code overflow="wrap" %}
```powershell
Get-CimInstance -Query "SELECT * FROM Win32_NTLogEvent WHERE Logfile = '<LogName>'"
```
{% endcode %}

List of available event logs and the number of records in each log:

```powershell
wmic nteventlog get LogFileName,NumberOfRecords
```

View specified event logs:

```powershell
wmic nteventlog where (LogFileName='<LogName>') get /format:list
```

Viewing Application logs:

```powershell
psloglist -s -t "\t" Application | findstr /n /i
```

Search for SID and username:

```powershell
psloglist -s -t "\t" -n 20 Security | findstr /n /i "SID"
```

EventID

```powershell
psloglist -s -t "\t" -r Security | findstr /n /i "4625"
```

EventID

```powershell
psloglist -s -t "\t" -r Security -i 4625
```

Format to text removes UTC:

```powershell
wevtutil qe Application "/q:*[System [(EventID=11707)]]" /rd:true /f:text
```

```powershell
wevtutil qe Application "/q:*[System [(EventID=11707)]]" /f:text
```

pstools show most recent logged in users: Type 10 Logons"

```powershell
psloglist "Security" -i 528 -s | find /i "Logon Type: 10"
```

10 newest System logs?:

```powershell
wevtutil qe System /c:10 /f:text
```

10 newest System logs?:

```powershell
psloglist -n 10 System
```

Collect informationn related to all Windows Event log instances containing successful logons, security log clearing and unexpected shutdowns -> desktop text file:

{% code overflow="wrap" %}
```powershell
$UserDirectory = (gi env:\userprofile).value Get-WinEvent -FilterHashtable @{Logname='security';ID=4624,517,6008} | select TimeCreated,ID,Message | ft -auto -wrap | out-file $UserDirectory\desktop\LogAnalysis.txt
```
{% endcode %}

Retrieve a list of USB devices that have been attached with the associated friendly device description:

{% code overflow="wrap" %}
```powershell
Get-ItemProperty -ea 0 hklm:\system\currentcontrolset\enum\usbstor\*\* | select FriendlyName,PSChildName
```
{% endcode %}

## <mark style="color:red;">Check for PS Logging (PS3+)</mark>

Verify logging:

```powershell
Get-Module Microsoft.* | Select Name, LogPipelineExecutionDetails
```

Enables Logging:

```powershell
Get-Module Microsoft.* | ForEach {$_.LogPipelineExecutionDetails = $True}
```

Disables Logging:

```powershell
Get-Module Microsoft.* | ForEach {$_.LogPipelineExecutionDetails = $False}
```

Registry Location:

{% code overflow="wrap" %}
```powershell
reg query "HKLM\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\PowerShell\ModuleLogging\EnableModuleLogging"
```
{% endcode %}

## <mark style="color:red;">EventID</mark>

Find all events with EventID 4624 (Logon events) in the Security log

```powershell
Get-EventLog -LogName Security -InstanceId 4624
```

Find all events with EventID 1001 (Windows Error Reporting) in the Application log

```powershell
Get-EventLog -LogName Application -InstanceId 1001
```

Find all events with EventID 4624 (Logon events) in the Security log

```powershell
Get-WinEvent -LogName Security | Where-Object { $_.Id -eq 4624 }
```

Find all events with EventID 1001 (Windows Error Reporting) in the Application log

```powershell
Get-WinEvent -LogName Application | Where-Object { $_.Id -eq 1001 }
```

This gives the most recent entry of the PowerShell EventLog with an Event ID of 800:

{% code overflow="wrap" %}
```powershell
Get-WinEvent -FilterHashtable @{LogName='Windows PowerShell';Id ='800'} -MaxEvents 1 | Select -Expand Message
```
{% endcode %}

Find all events with EventID 4624 (Logon events) in the Security log

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_NTLogEvent -Filter "LogFile='Security' AND EventCode=4624"
```
{% endcode %}

Find all events with EventID 1001 (Windows Error Reporting) in the Application log

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_NTLogEvent -Filter "LogFile='Application' AND EventCode=1001"
```
{% endcode %}

Find all events with EventID 4624 (Logon events) in the Security log

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_NTLogEvent -Filter "LogFile='Security' AND EventCode=4624"
```
{% endcode %}

Retrieve events with EventID 4624 (Logon events) from the Security log

{% code overflow="wrap" %}
```powershell
Get-WmiObject -Query "SELECT * FROM Win32_NTLogEvent WHERE Logfile='Security' AND EventCode=4624"
```
{% endcode %}

## <mark style="color:red;">Content/Keywords</mark>

Find all events in the Security log that contain the username "JohnDoe"

```powershell
Get-EventLog -LogName Security | Where-Object { $_.Message -like "*JohnDoe*" }
```

Find all events in the Application log that have the keyword "Critical"

{% code overflow="wrap" %}
```powershell
Get-EventLog -LogName Application -EntryType "Error", "Warning", "Information" | Where-Object { $_.Message -like "*Critical*" }
```
{% endcode %}

Find all events in the System log that contain the word "error"

```powershell
Get-WinEvent -LogName System | Where-Object { $_.Message -like "*error*" }
```

Find all events in the System log that have the keyword "disk"

```powershell
Get-WinEvent -LogName System | Where-Object { $_.Keywords -band 0x4 }
```

## <mark style="color:red;">Date Range</mark>

Retrieve events in the Security log that occurred between two specific dates

```powershell
$StartDate = Get-Date "2023-01-01"
```

```powershell
$EndDate = Get-Date "2023-12-31"
```

```powershell
Get-EventLog -LogName Security -After $StartDate -Before $EndDate
```

Retrieve events in the Application log within the specified date range

```powershell
$StartTime = (Get-Date) - (New-TimeSpan -Days 7)
```

```powershell
$EndTime = Get-Date
```

```powershell
Get-EventLog -LogName Application -After $StartTime -Before $EndTime
```

Retrieve events from all logs that occurred between two specific dates

```powershell
$StartDate = Get-Date "2023-01-01"
```

```powershell
$EndDate = Get-Date "2023-12-31"
```

```powershell
Get-EventLog -LogName * -After $StartDate -Before $EndDate
```

Find events within a specific date-time range in the System log

```powershell
$StartTime = Get-Date "2023-01-01T00:00:00"
```

```powershell
$EndTime = Get-Date "2023-12-31T23:59:59"
```

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_NTLogEvent -Filter "LogFile='System' AND TimeGenerated >= '$StartTime' AND TimeGenerated <= '$EndTime'"
```
{% endcode %}

Retrieve events in the Application log within the specified date range

```
$StartTime = (Get-Date "2023-01-01 00:00:00")
$EndTime = (Get-Date "2023-01-02 23:59:59")

Get-WinEvent -LogName Application -FilterHashtable @{
    LogName='Application';
    StartTime=$StartTime;
    EndTime=$EndTime
}
```

Retrieve events within the specified date and time range from the Application log

{% code overflow="wrap" %}
```
$StartTime = "2023-01-01T00:00:00Z"
$EndTime = "2023-01-02T23:59:59Z"

Get-WmiObject -Query "SELECT * FROM Win32_NTLogEvent WHERE Logfile='Application' AND TimeGenerated >= '$StartTime' AND TimeGenerated <= '$EndTime'"
```
{% endcode %}
