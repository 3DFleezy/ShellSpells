# Output Formatting / Filtering

## Format

### Table

```powershell
Get-Process | Format-Table -Property *
```

```powershell
Get-Process | Format-Table -Property ID,Name,Responding
```

```powershell
Get-Process | Format-Table *
```

```powershell
Get-Process | ft 
```

### -Wrap

```powershell
Get-Command | Select-Object Name,Source | ft -Wrap
```

Format Process list with Virtual and Paged Memory in MBs and no Decimals

Understand the "Name" is a property from Get-Process, but also a property for Format-Table. See next example if that doesn't make sense.

{% code overflow="wrap" %}
```powershell
get-process | Format-Table name,id, @{name='VM(MB)'; expression={$_.VM / 1MB -as [int]}}, @{name='PM(MB)'; expression={$_.PM / 1MB -as [int]}}
```
{% endcode %}

Formatting Process List to Include Select Fields:

```powershell
Get-Process | Format-Table Name,ID,Responding -Wrap
```

### List

Format-List is another way of displaying the properties of an object. Unlike get-member, Format-List (fl) will also display the values for those properties so that you can see what kind of information each property contains

Most parameters are the same as Format-Table.

<table data-header-hidden data-full-width="true"><thead><tr><th width="388">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>gci | Format-List -property name</code></mark></td><td>Formatting output of a command (Format-List)</td></tr><tr><td><mark style="color:yellow;"><code>ls | Format-List -property name</code></mark></td><td>Formatting output of a command (Format-List)</td></tr><tr><td><mark style="color:yellow;"><code>Get-Help Format-List</code></mark></td><td>Formats the help output as a list</td></tr></tbody></table>

### Wide

It’s able to display only the values of a single property, so its -Property parameter accepts only one property name, not a list, and it can’t accept wildcards.

```powershell
Get-Process | Format-Wide name -col 4
```

Formats the output to a specified width and writes to a new file.

```powershell
Get-Content C:\path\to\file.txt | Out-File C:\path\to\newfile.txt -Width 120
```

### GroupBy

{% code overflow="wrap" %}
```powershell
Get-AzVM -Status | Sort-Object PowerState | ft -Property Name,Location,ResourceGroupName -GroupBy PowerState
```
{% endcode %}

### Paging

Paginating output:

```powershell
gci -recurse | Out-Host -paging
```

## Select-Object

<table data-header-hidden data-full-width="true"><thead><tr><th width="429">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Select-Object</code></mark>or <mark style="color:yellow;"><code>Select</code></mark></td><td>Selects a specified property from an object.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process | Select Name,ID,CPU,PM</code></mark></td><td>Selects multiple properties.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process | Select -First 10</code></mark></td><td>Selects first 10.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process | Select -Last 10</code></mark></td><td>Selects last 10.</td></tr></tbody></table>

Displays the Get-Process Properties of 'Name, ID, Path' for every process

```powershell
Get-Process | Select-Object Name, ID, path
```

## Where-Object

<table data-header-hidden data-full-width="true"><thead><tr><th width="494">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Where-Object</code></mark></td><td>Filters objects out of the pipeline.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Content C:\path\to\file.txt | Where-Object {$_ -match "pattern"}</code></mark></td><td>Filters lines that match a specific pattern.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process | Where-Object {$_.name -eq "notepad"}</code></mark></td><td>Where-Object condition (alias where or ?).</td></tr></tbody></table>

## Creating Custom Columns and List Entries

You can use this to provide a column header that’s different from the property name being displayed:

{% code overflow="wrap" %}
```powershell
Get-AzStorageAccount | Format-Table @{name='Name';expression={$_.StorageAccountName}},Location,ResourceGroupName
```
{% endcode %}

This creates a special hash table to create a custom column that will be labeled VM(MB) and changes the value of that property to MBs. It then converst that value to a whole number rather than a decimal.

{% code overflow="wrap" %}
```powershell
Get-Process | Format-Table Name, @{name='VM(MB)';expression={$_.VM / 1MB -as [int]}}
```
{% endcode %}

NOTE: PowerShell recognizes the shortcuts KB, MB, GB, TB, and PB as denoting kilobyte, megabyte, gigabyte, terabyte, and petabyte, respectively

Format custom number of columns. Need to use `Format-Wide`:

```powershell
get-childitem C:\Users\fleezy\ | Format-List Name -col 4
```

Format list that contains specific fields with one custom field:

```powershell
gci $PSHOME | Format-List Name,VersionInfo,@{name='Size'; expression={$_.Length}}
```

Format custom headers for Get-Module's Name and Version:

{% code overflow="wrap" %}
```powershell
Get-Module | Format-Table @{Name='ModuleName'; expression={$_.Name}}, @{Name='ModuleVersion'; expression={$_.Version}}
```
{% endcode %}
