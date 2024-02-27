# Extract Content

## <mark style="color:red;">Pattern Match</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="608">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find /i "keyword" file.txt</code></mark></td><td>Find text, case-insensitive.</td></tr><tr><td><mark style="color:yellow;"><code>sls -path [file] -pattern [string]</code></mark></td><td>Find strings in a file (PowerShell)</td></tr><tr><td><mark style="color:yellow;"><code>select-string -path [file] -pattern [string]</code></mark></td><td>Find strings in a file (PowerShell)</td></tr><tr><td><mark style="color:yellow;"><code>Select-String -path c:\\users \\\*.txt –pattern password</code></mark></td><td>Find strings in a file (PowerShell)</td></tr><tr><td><mark style="color:yellow;"><code>findstr "pattern" C:\path\to\file.txt</code></mark></td><td>Find matching lines (CMD)</td></tr><tr><td><mark style="color:yellow;"><code>type C:\path\to\file.txt | findstr "pattern"</code></mark></td><td>Find matching lines (CMD)</td></tr><tr><td><mark style="color:yellow;"><code>Get-Content file.txt | Select-String -Pattern "keyword"</code></mark></td><td>Find strings in a file (PowerShell)</td></tr></tbody></table>

Find text within a file:

```powershell
gci -recurse c:\\users -file | % {Select-String -path $ \_ -pattern password}
```

Search a file's contents for Polo. This also splits the file from one line to a newline for each word:

```powershell
((Get-Content .\countpolos).split(" ")) | select-string \bpolo\b 
```

Filter lines that contain a specific string:

{% code overflow="wrap" %}
```powershell
Get-Content C:\path\to\file.txt | Where-Object { $_ -match "specific string" } | Set-Content C:\path\to\filteredfile.txt
```
{% endcode %}

Don't forget to use <mark style="color:yellow;">`-ErrorAction SilentlyContinue`</mark>

## <mark style="color:red;">Line Numbers</mark>

Displays the content of a file starting from the 11th line:

```powershell
more +10 C:\file.txt
```

## <mark style="color:red;">Unique / Deduplicate</mark>

Remove duplicate lines from a file:

{% code overflow="wrap" %}
```powershell
Get-Content C:\path\to\file.txt | Sort-Object | Get-Unique | Set-Content C:\path\to\uniquefile.txt
```
{% endcode %}

Reads the file, sorts the lines, removes duplicates, and saves the result to a new file using PowerShell.

{% code overflow="wrap" %}
```powershell
Get-Content C:\path\to\file.txt | Sort-Object | Get-Unique | Set-Content C:\path\to\outputfile.txt 
```
{% endcode %}

Filters lines matching a specific pattern, removes duplicates, and saves to a new file using PowerShell.

{% code overflow="wrap" %}
```powershell
(Get-Content C:\path\to\file.txt) -match 'pattern' | Select-Object -Unique | Set-Content C:\path\to\filteredfile.txt 
```
{% endcode %}

For CSV files, sorts entries based on a specific column, removes duplicates, and saves the result to a new CSV file using PowerShell.

{% code overflow="wrap" %}
```powershell
Import-Csv C:\path\to\file.csv | Sort-Object -Property ColumnName -Unique | Export-Csv C:\path\to\outputfile.csv -NoTypeInformation
```
{% endcode %}

Groups lines, identifies duplicates, selects one occurrence of each duplicate, and saves the result using PowerShell.

{% code overflow="wrap" %}
```powershell
Get-Content C:\path\to\file.txt | Group-Object | Where-Object { $_.Count -gt 1 } | ForEach-Object { $_.Group | Select-Object -First 1 } | Set-Content C:\path\to\outputfile.txt
```
{% endcode %}
