# Date/Time

## <mark style="color:red;">Commands</mark>

### <mark style="color:purple;">Date & Time</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>date /t &#x26;&#x26; time /t</code></mark></td><td>Date and time (/t prevents changing value)</td></tr><tr><td><mark style="color:yellow;"><code>cmd /c "date /t &#x26;&#x26; time /t"</code></mark></td><td>Date and time</td></tr><tr><td><mark style="color:yellow;"><code>wmic os get localdatetime</code></mark></td><td>Date and time</td></tr><tr><td><mark style="color:yellow;"><code>wmic path Win32_LocalTime get</code></mark></td><td>Date and time</td></tr><tr><td><mark style="color:yellow;"><code>powershell Get-Date</code></mark></td><td>Date and time</td></tr><tr><td><mark style="color:yellow;"><code>powershell [System.DateTime]::Now</code></mark></td><td>Date and time</td></tr><tr><td><mark style="color:yellow;"><code>powershell [System.DateTime]::UtcNow</code></mark></td><td>Date and time in UTC</td></tr><tr><td><mark style="color:yellow;"><code>powershell (Get-Date).ToLongDateString()</code></mark></td><td>Date in long format</td></tr><tr><td><mark style="color:yellow;"><code>powershell (Get-Date).ToLongTimeString()</code></mark></td><td>Time in long format</td></tr><tr><td><mark style="color:yellow;"><code>powershell (Get-Date).DayOfWeek</code></mark></td><td>Day of the week</td></tr><tr><td><mark style="color:yellow;"><code>powershell Get-WmiObject Win32_LocalTime</code></mark></td><td>Time</td></tr><tr><td><mark style="color:yellow;"><code>powershell Get-CimInstance Win32_LocalTime</code></mark></td><td>Time details</td></tr></tbody></table>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object LocalDateTime
```

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_OperatingSystem | Select-Object -ExpandProperty LocalDateTime
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
Get-CimInstance -ClassName Win32_LocalTime | Select-Object -Property Hour, Minute, Second, caption
```
{% endcode %}



### <mark style="color:purple;">Timezone</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tzutil /g</code></mark></td><td>Timezone</td></tr><tr><td><mark style="color:yellow;"><code>wmic timezone get caption</code></mark></td><td>Timezone</td></tr><tr><td><mark style="color:yellow;"><code>wmic path Win32_TimeZone get Caption</code></mark></td><td>Timezone</td></tr><tr><td><mark style="color:yellow;"><code>powershell Get-TimeZone</code></mark></td><td>Timezone</td></tr><tr><td><mark style="color:yellow;"><code>wmic os get currenttimezone /format:list</code></mark></td><td>Timezone details</td></tr><tr><td><mark style="color:yellow;"><code>powershell [System.TimeZoneInfo]::Local</code></mark></td><td>Timezone details</td></tr><tr><td><mark style="color:yellow;"><code>powershell Get-WmiObject Win32_TimeZone</code></mark></td><td>Timezone details</td></tr><tr><td><mark style="color:yellow;"><code>powershell Get-CimInstance Win32_TimeZone</code></mark></td><td>Timezone details</td></tr><tr><td><mark style="color:yellow;"><code>[System.TimezoneInfo]::Local</code></mark></td><td>Timezone details</td></tr></tbody></table>



## <mark style="color:red;">Registry Locations</mark>

Time Zone Information: <mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation</mark> \
This key contains information about the currently set timezone, including the name, bias, and daylight saving time settings.

Time and Date Formats: \
<mark style="color:orange;">HKEY\_CURRENT\_USER\Control Panel\International</mark> \
This key stores user-specific settings related to date and time formats, such as short date format, long date format, time format, and first day of the week.

<mark style="color:orange;">Internet Time Settings: HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\DateTime\Servers</mark> \
This key contains information about the Internet time servers that Windows can synchronize with.

Automatic Time Synchronization Settings: <mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Parameters</mark> \
This key includes parameters for the Windows Time service, which is responsible for synchronizing the computer's clock with a network time protocol (NTP) server.

Daylight Saving Time Update Configuration: <mark style="color:orange;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones</mark> \
This key contains subkeys for each time zone, including information about daylight saving time rules and adjustments.

User-specific Time Zone Settings (if different from the system default): <mark style="color:orange;">HKEY\_CURRENT\_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones</mark> \
Similar to the system-wide time zone settings, but specific to the current user.
