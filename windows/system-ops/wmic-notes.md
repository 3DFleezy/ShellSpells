# WMIC Notes

WMI designed to give applications access to managed objects (Processes, reg keys, files, etc)

WMI breakdown:&#x20;

<mark style="color:orange;">**Consumers**</mark>: Management Applications (WMI Consumers)

<mark style="color:orange;">**Infrastructure**</mark>: WMI Core (CIM Object Manager) -> Database

<mark style="color:orange;">**Providers**</mark>: WMI Providers -> Managed Objects

The easiest way to access these Managed objects is with <mark style="color:yellow;">`wmic`</mark>. \
<mark style="color:yellow;">`wmic`</mark> command should be run in CMD prompt. \
Not all commands work in PS.

To use WMI you need to know 3 things:

1. Available classes
2. Class names
3. Class properties and methods

List available WMI/CIM classes:&#x20;

```powershell
Get-CimClass 
```

OR

```powershell
Get-WMIObject -List -Namespace root\wmi
```



To query a specific Class for Properties and Methods:

```powershell
Get-CimInstance -ClassName [Class Name] | Get-Member
```

Or

```powershell
Get-WMIObject -Class [classname] | get-member
```



To search through a specific class and filter on a string

```powershell
Get-CimClass -Classname *[search string]*
```

Or

```powershell
Get-WMIObject -List | Where-Object {$_.name -match '[SearchString]'}
```



Filter output based on property value

```powershell
Get-CimInstance -ClassName [classname] -Filter "[filter]"
```

Example:

```powershell
Get-CimInstance -ClassName [classname] -Filter "name like 'PowerShell'"
```

OR

```powershell
Get-WMIObject -Query "Select * from [classname]"
```



Almost every command will have a <mark style="color:yellow;">`list brief`</mark> and <mark style="color:yellow;">`list full`</mark> option. Results vary.

Filtering and using <mark style="color:yellow;">`get`</mark> with WMIC: \
<mark style="color:yellow;">`get`</mark> allows you to specify what field you want. \
This is the alternative to <mark style="color:yellow;">`Get-CimInstance`</mark>.

Get process information:

{% code overflow="wrap" %}
```powershell
wmic process get name,processid,parentprocessid,executablepath,commandline /format:list
```
{% endcode %}

Get a single process info:

{% code overflow="wrap" %}
```powershell
wmic process where name="wmic.exe" get processid,executablepath,commandline
```
{% endcode %}
