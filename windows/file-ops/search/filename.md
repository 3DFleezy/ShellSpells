# Filename

## <mark style="color:red;">Local</mark>

### <mark style="color:purple;">Filenames</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>where /R C:\Users\ "keyword*"</code></mark></td><td>Recursive search for a keyword (CMD only).</td></tr><tr><td><mark style="color:yellow;"><code>dir /s /b &#x3C;filename></code></mark></td><td>Recursive search for a filename with full path.</td></tr><tr><td><mark style="color:yellow;"><code>dir &#x3C;filename>*</code></mark></td><td>Lists files in the current directory with a name starting with <mark style="color:yellow;"><code>&#x3C;filename></code></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>dir &#x3C;path>\&#x3C;filename>*</code></mark></td><td>Lists files in the specified path with a name starting with <mark style="color:yellow;"><code>&#x3C;filename></code></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ChildItem C:\Users *readme* -Recurse</code></mark></td><td>Recursive search with PowerShell.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ChildItem -Path &#x3C;path> -Filter &#x3C;filename>*</code></mark></td><td>Lists files in the specified path matching the filter <mark style="color:yellow;"><code>&#x3C;filename>*</code></mark>. More efficient than <code>-Include</code>.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ChildItem -Path &#x3C;path> -Include &#x3C;filename>*</code></mark></td><td>Lists files in the specified path including files matching the pattern <mark style="color:yellow;"><code>&#x3C;filename>*</code></mark>. Allows more complex patterns than <code>-Filter</code>.</td></tr><tr><td><mark style="color:yellow;"><code>Get-ChildItem -Path &#x3C;path> -Exclude &#x3C;filename>*</code></mark></td><td>Lists files in the specified path excluding files matching the pattern <mark style="color:yellow;"><code>&#x3C;filename>*</code></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>findstr /s /i /m "search_string"</code></mark></td><td>Recursive search for a string (CMD only), case-insensitive.</td></tr><tr><td><mark style="color:yellow;"><code>for /R %f in (&#x3C;filename>*) do @echo %f</code></mark></td><td>Recursive for-loop in CMD.</td></tr><tr><td><mark style="color:yellow;"><code>Where-Object { $_.Name -like "&#x3C;filename>*" }</code></mark></td><td>Filters objects by name match in PowerShell.</td></tr></tbody></table>

Find files by name/partial name (WMI).

```powershell
Get-CimInstance -ClassName CIM_DataFile -Filter "Name LIKE '%<filename>%'"
```

Find file names and paths by name/partial name (WMI).

```powershell
wmic datafile where Name like '%<filename>%' get Name, FileName
```

Find all files with a particular name:

```powershell
Get-ChildItem "C:\\Users\\" recurse -include \*passwords\*.txt
```

Searches only non-system files recursively:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <path> -Recurse | Where-Object { $_.Attributes -match 'Archive' } | Select-String -Pattern <string>
```
{% endcode %}

### <mark style="color:purple;">File Extensions</mark>

Multiple extensions:

```powershell
Get-ChildItem -Path C:\Documents -Recurse -Include "*.txt", "*.docx"
```

### <mark style="color:purple;">Remote</mark>

Find applications that begin with Google:

{% code overflow="wrap" %}
```powershell
Get-WmiObject Win32_Product -computername win7 -credential fred -filter "Name like '%Google%'"
```
{% endcode %}

Uninstall applications that begin with Google:

{% code overflow="wrap" %}
```powershell
(Get-WmiObject Win32_Product -computername win7 -credential fred -filter "Name like '%Google%'").Uninstall()
```
{% endcode %}

## <mark style="color:red;">Content</mark>

Go-to Command:

```powershell
findstr /s /i /n /p "keyword" *.* 
```

<mark style="color:yellow;">`/s`</mark> Recursive

<mark style="color:yellow;">`/i`</mark> Case-insensitive

<mark style="color:yellow;">`/n`</mark> Displays line numbers with output

<mark style="color:yellow;">`/p`</mark> Skips files with non-printable characters

<mark style="color:yellow;">`*.*`</mark> Searches all files

Recursive:

```powershell
gci -Recurse | sls "keyword"
```

Recursive, case-insensitive:

```powershell
findstr /s /i "keyword" *.*
```

Searches for entire lines matching the string:

```powershell
findstr /s /m <string> <path>
```

Searches only text files recursively:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <path> -Recurse -Include *.txt | Select-String -Pattern <string>
```
{% endcode %}

Searches all files for a keyword across the entire C: drive, returning only files that contain the keyword:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path C:\ -Recurse | Where-Object { $_ | Select-String -Pattern "keyword" -Quiet }
```
{% endcode %}

Searches for a keyword in files under a specified directory and lists each file only once if the keyword is found:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path C:\path\to\directory -Recurse | Select-String -Pattern "keyword" -List
```
{% endcode %}

Additional Tips:

Use regular expressions with findstr for advanced pattern matching.

## <mark style="color:red;">Users (Owners)</mark>

Lists files owned by a specific username, recursively:

```powershell
dir <path> /q /s /o:n | findstr /i "Owner: <username>"
```

```powershell
Get-ChildItem -Path <path> -Recurse -Owner <username>
```

{% code overflow="wrap" %}
```powershell
Get-ChildItem <Path> -Recurse | ForEach-Object { Get-Acl $_.FullName } | Select-Object Path, Owner
```
{% endcode %}

Lists files owned by a specific username on the local system:

```powershell
wmic datafile where owner='<username>' get Name, FileName
```

Lists files where the owner's SID (Security Identifier) matches the specified username:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <path> -Recurse -ErrorAction SilentlyContinue | Where-Object { $_.GetAccessControl().Owner.Owner -eq "<username>" }
```
{% endcode %}

Lists files created by a specific username within a specified date range:

{% code overflow="wrap" %}
```powershell
wmic datafile where (owner='<username>' and CreationDate >= <start_date> and CreationDate <= <end_date>) get Name, FileName
```
{% endcode %}

Lists files with specific permissions for a user, recursively:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <path> -Recurse -File | Where-Object { $_.GetAccessControl().Access.IdentityReference -like "<username>*" } | Select-Object FullName
```
{% endcode %}

### <mark style="color:purple;">Windows Search (GUI)</mark>

Open File Explorer, navigate to the desired directory.

In the search bar, type <mark style="color:yellow;">`created:<username>`</mark> (replace with the actual username).

Optionally, filter by date range using created:<mark style="color:yellow;">`<start_date>..<end_date>`</mark>.

Additional Tips:

Replace with the actual username you're searching for.

Use wildcards (\*) in the username to match partial names.

For a case-insensitive search in PowerShell, use <mark style="color:yellow;">`-imatch`</mark> or <mark style="color:yellow;">`-ilike`</mark> instead of <mark style="color:yellow;">`=`</mark>.
