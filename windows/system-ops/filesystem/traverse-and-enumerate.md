# Traverse & Enumerate

You can traverse the Registry like a filesystem thanks to PSProviders.

| <mark style="color:yellow;">`Get-location`</mark>                      | Present dir                                   |
| ---------------------------------------------------------------------- | --------------------------------------------- |
| <mark style="color:yellow;">`Set-location`</mark>                      | Change dir                                    |
| <mark style="color:yellow;">`cd HKLM:\\`</mark>                        | Navigate the Windows registry                 |
| <mark style="color:yellow;">`set-location -Path hkcu:`</mark>          | Change current location to the HCKU Hive      |
| <mark style="color:yellow;">`set-location -Path software`</mark>       | Change to the Software Key                    |
| <mark style="color:yellow;">`dir /tc /od c:\\windows\\system32`</mark> | List all order by date and list creation time |
| <mark style="color:yellow;">`dir /q`</mark>                            | Shows file owners                             |

Recursively list the paths of all files in a directory and its subdirectories:

```powershell
forfiles /p "C:\path\to\directory" /s /c "cmd /c echo @path"
```

Find applications that begin with Google:

{% code overflow="wrap" %}
```powershell
Get-WmiObject Win32_Product -computername win7 -credential fred -filter "Name like '%Google%'"
```
{% endcode %}

Lists the Name and MAC times of C:\Windows:

{% code overflow="wrap" %}
```powershell
wmic fsdir where (name="C:\\\\Windows") get lastmodified, lastaccessed, creationdate, name
```
{% endcode %}

Show file renames that are pending:

{% code overflow="wrap" %}
```powershell
reg query "HKLM\System\CurrentControlSet\Control\Session Manager\FileRenameOperations"
```
{% endcode %}

Show shell, default domain name, default user name, legal notice, etc.:

{% code overflow="wrap" %}
```powershell
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon"
```
{% endcode %}
