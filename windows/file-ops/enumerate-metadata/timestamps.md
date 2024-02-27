# Timestamps

## Commands

<table data-header-hidden data-full-width="true"><thead><tr><th width="507">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>dir /tw &#x3C;file></code></mark></td><td>Last Modified</td></tr><tr><td><mark style="color:yellow;"><code>dir /ta &#x3C;file></code></mark></td><td>Last Access</td></tr><tr><td><mark style="color:yellow;"><code>dir /tc &#x3C;file></code></mark></td><td>Creation</td></tr><tr><td><mark style="color:yellow;"><code>Get-Item &#x3C;file> | Select-Object LastWriteTime</code></mark></td><td>Last Modified</td></tr><tr><td><mark style="color:yellow;"><code>Get-Item &#x3C;file> | Select-Object LastAccessTime</code></mark></td><td>Last Access</td></tr><tr><td><mark style="color:yellow;"><code>Get-Item &#x3C;file> | Select-Object CreationTime</code></mark></td><td>Creation</td></tr></tbody></table>

Print the last modified date of all files in a directory

```powershell
forfiles /p "C:\path\to\directory" /c "cmd /c echo @file @fdate"
```

Lists the Name and MAC times of C:\Windows:

{% code overflow="wrap" %}
```powershell
wmic fsdir where (name="C:\\Windows") get lastmodified, lastaccessed, creationdate, name
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
wmic datafile where name="C:\\FileOfInterest' get creationdate,lastmodified,lastaccessed
```
{% endcode %}

View Creation Date of Processes w/ Proper Timestamps:

{% code overflow="wrap" %}
```powershell
Get-WmiObject win32_process | select processname,@{NAME='CreationDate';EXPRESSION={$_.ConvertToDateTime($_.CreationDate)}},ProcessId,CommandLine |sort CreationDate -desc | format-table -auto -wrap
```
{% endcode %}

Search a date range:

{% code overflow="wrap" %}
```powershell
Get-ChildItem 'C:\' -recurse -include @("*.*") | Where-Object { $_.CreationTime -ge "03/01/2014" -and $_.CreationTime -le "04/14/2015" }
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
wmic datafile where "drive='c:' and path like '%\\%' and lastmodified>'20140414233423.000000-240' and lastmodified<'20140420233445.000000-240'" get name
```
{% endcode %}

Get time stamp of malicious exe and search for other files around the same time, going up or down a minute or two as needed

```powershell
dir /s /t:c C:\ | find /I "nc.exe" 
```

## Remote

{% code overflow="wrap" %}
```powershell
wmic /node:xp /user:xp\administrator /password:L33tHax0r datafile where name='c:\\windows\\system32\\logon.scr' list full
```
{% endcode %}

## Timestamp Updates

<mark style="color:orange;">Create Time</mark>

The create timestamp is updated anytime a file or directory is created from scratch or a copy is made.

<mark style="color:orange;">Modify Time</mark>

The modification timestamp is updated anytime a file or directory is changed.

<mark style="color:orange;">Access Time</mark>

The access timestamp is updated anytime the contents (including metadata) of a file or directory is touched to perform an action.

<mark style="color:orange;">Entry Modify Time</mark>

The entry modified timestamp refers to the time when the Master File Table (MFT) entry itself was modified.

Creating a folder updates the - Modified, Access and Create Times (for the folder)

Creating a file updates the - Modified, Access and Creat Times (for the file)

Creating a file within a folder updates the - Modified and Access Times (for the folder)



Modifying a file updates the - Modified and Access Times (for the file)

Modifying a file updates the - Modified and Access Times (for the folder)



Moving a file into a folder/directory updates the - Modified and Access Times (for the folder/dir)

Moving a file into a folder/directory updates the - Access Time (for the file)



Copying a file into a folder/directory updates the - Access Time (for the directory the file was copied FROM)

Copying a file into a folder/directory updates the - Modified and Access Time (for the directory the file was copied TO)

The difference between a copy and move is that a COPY will create a new file at the destination and results in multiple files and a MOVE will create a new file at the destination and then erases the original file from its location by updating the Master File Table (MFT) to point to the new location.

The default action when a Drag and Drop function is performed within the same partition is a MOVE and when performed on a different partition is a COPY.

## Enable/Disable Last Access Update TIme

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate</mark>

\-> value of 1 means disabled (default in Vista+)

\-> value of 0 means enabled (default in XP and earlier -if the key exists)

## Registry Locations

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation</mark>

Contains information about the current time zone settings, including bias, standard time, and daylight saving time adjustments.

<mark style="color:blue;">HKEY\_USERS.DEFAULT\Control Panel\International</mark>

Stores user-specific international settings, including date and time formats, for the default user profile.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Control Panel\International</mark>

Contains the current user's international settings, including date and time formats, reflecting the user's locale preferences.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Parameters</mark>

Holds configuration parameters for the Windows Time service, which is responsible for time synchronization in Windows.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config</mark>

Contains additional configuration settings for the Windows Time service, such as time correction settings and polling intervals.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders</mark>

Stores settings for various time providers used by the Windows Time service for time synchronization.
