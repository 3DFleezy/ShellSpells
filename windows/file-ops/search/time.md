# Time

## <mark style="color:red;">Accessed Time</mark>

All accessed times:

```powershell
dir /ta
```

All accessed times, recursive:

```powershell
dir /ta /s
```

Accessed on <mark style="color:orange;">EXACT</mark> date:

```powershell
dir /ta /s | findstr "01/17/2024"
```

Accessed on <mark style="color:orange;">EXACT</mark> date:

```powershell
Get-ChildItem -Path C:\ -Recurse -Filter "*.*" -LastAccessTime "02/16/2024"
```

Accessed <mark style="color:orange;">AFTER</mark>, recursive:

{% code overflow="wrap" %}
```powershell
Get-ChildItem "C:\path" -Recurse | Where-Object { $_.LastAccessTime -gt "MM/DD/YYYY" }
```
{% endcode %}

Accessed <mark style="color:orange;">BEFORE</mark>, recursive:

{% code overflow="wrap" %}
```powershell
Get-ChildItem "C:\path" -Recurse | Where-Object { $_.LastAccessTime -lt "MM/DD/YYYY" }
```
{% endcode %}

Accessed within date range:

{% code overflow="wrap" %}
```powershell
$startDate = Get-Date "MM/DD/YYYY"; $endDate = Get-Date "MM/DD/YYYY"; Get-ChildItem -Path "C:\path" -Recurse | Where-Object { $_.LastAccessTime -gt $startDate -and $_.LastAccessTime -lt $endDate }
```
{% endcode %}

## <mark style="color:red;">Modified Time</mark>

All modified times:

```powershell
dir /tw
```

All modified times, recursive:

```powershell
dir /tw /s
```

Modified on <mark style="color:orange;">EXACT</mark> date:

```powershell
dir /tw /s | findstr "01/17/2024"
```

Modified on <mark style="color:orange;">EXACT</mark> date `/m` allows wildcards:

```powershell
forfiles /P /M "*.*" /S /D "-02/16/2024"
```

Modified on <mark style="color:orange;">EXACT</mark> date:

```powershell
Get-ChildItem -Path C:\ -Recurse -Filter "*.*" -LastWriteTime "02/16/2024"
```

Modified <mark style="color:orange;">AFTER</mark>, recursive:

```powershell
forfiles /P "C:\path" /S /D +MM/DD/YYYY
```

Modified <mark style="color:orange;">AFTER</mark>, recursive:

{% code overflow="wrap" %}
```powershell
Get-ChildItem "C:\path" -Recurse | Where-Object { $_.LastWriteTime -gt "MM/DD/YYYY" }
```
{% endcode %}

Modified <mark style="color:orange;">BEFORE</mark>, recursive:

```powershell
forfiles /P "C:\path" /S /D -MM/DD/YYYY
```

Modified <mark style="color:orange;">BEFORE</mark>, recursive:

{% code overflow="wrap" %}
```powershell
Get-ChildItem "C:\path" -Recurse | Where-Object { $_.LastWriteTime -lt "MM/DD/YYYY" }
```
{% endcode %}

Modified within date range:

{% code overflow="wrap" %}
```powershell
$startDate = Get-Date "MM/DD/YYYY"; $endDate = Get-Date "MM/DD/YYYY"; Get-ChildItem -Path "C:\path" -Recurse | Where-Object { $_.LastWriteTime -gt $startDate -and $_.LastWriteTime -lt $endDate }
```
{% endcode %}

## <mark style="color:red;">Creation Time</mark>

All creation times:

```powershell
dir /tc
```

All creation times, recursive:

```powershell
dir /tc /s
```

Creation on <mark style="color:orange;">EXACT</mark> date:

```powershell
dir /tc /s | findstr "01/17/2024"
```

Creation on <mark style="color:orange;">EXACT</mark> date:

```powershell
Get-ChildItem -Path C:\ -Recurse -Filter "*.*" -CreationTime "02/16/2024"
```

Creation <mark style="color:orange;">AFTER</mark>, recursive:

{% code overflow="wrap" %}
```powershell
Get-ChildItem "C:\path" -Recurse | Where-Object { $_.CreationTime -gt "MM/DD/YYYY" }
```
{% endcode %}

Creation <mark style="color:orange;">BEFORE</mark>, recursive:

{% code overflow="wrap" %}
```powershell
Get-ChildItem "C:\path" -Recurse | Where-Object { $_.CreationTime -lt "MM/DD/YYYY" }
```
{% endcode %}

Created within date range:

{% code overflow="wrap" %}
```powershell
$startDate = Get-Date "MM/DD/YYYY"; $endDate = Get-Date "MM/DD/YYYY"; Get-ChildItem -Path "C:\path" -Recurse | Where-Object { $_.CreationTime -gt $startDate -and $_.CreationTime -lt $endDate }
```
{% endcode %}

## <mark style="color:red;">Metadata Change Time</mark>

Combining FORFILES and PowerShell:

{% code overflow="wrap" %}
```powershell
forfiles /S /M "*.*" /C "cmd /c powershell -NoProfile (Get-ChildItem -Path %p).LastWriteTimeUtc -ne (Get-ChildItem -Path %p).CreationTimeUtc"
```
{% endcode %}

Explanation:

<mark style="color:yellow;">`FORFILES /S /M "*.*"`</mark> iterates through files recursively.

<mark style="color:yellow;">`/C "cmd /c ..."`</mark> executes a command for each file.

PowerShell within the command checks if the <mark style="color:orange;">LastWriteTimeUtc</mark> differs from <mark style="color:orange;">CreationTimeUtc</mark>, indicating metadata change.

{% hint style="warning" %}
This is not definitive.
{% endhint %}

The last write time can be different than the creation time if the file content was modified.
