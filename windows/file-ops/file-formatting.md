# File Formatting

## Convert Format

<table data-header-hidden data-full-width="false"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ConvertTo-Csv</code></mark></td><td>Converts to CSV</td></tr><tr><td><mark style="color:yellow;"><code>ConvertTo-Html</code></mark></td><td>Converts to HTML. This will reveal all properties.</td></tr><tr><td><mark style="color:yellow;"><code>ConvertTo-Json</code></mark></td><td>Converts to JSON and reveals **nested properties</td></tr><tr><td><mark style="color:yellow;"><code>ConvertTo-Xml</code></mark></td><td>Converts to XML</td></tr></tbody></table>

Example on Converting files To and from:

```powershell
Get-Process | ConvertTo-Json | Out-File procs.json
```

```powershell
Get-Content ./procs.json | ConvertFrom-Json
```

## Import/Export

<table data-header-hidden data-full-width="true"><thead><tr><th width="504">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Get-Process | Export-Csv procs.csv</code></mark></td><td>Exporting output to CSV</td></tr><tr><td><mark style="color:yellow;"><code>Export-Csv &#x3C;filename.csv> -NoClobber</code></mark></td><td>Does not overwrite the file</td></tr><tr><td><mark style="color:yellow;"><code>Export-CSV &#x3C;filename.csv> -UseCulture</code></mark></td><td>Uses the system’s default separator rather than a comma.</td></tr><tr><td><mark style="color:yellow;"><code>Import-Clixml</code></mark></td><td>Imports XML file to be read in PS</td></tr><tr><td><mark style="color:yellow;"><code>Import-Csv</code></mark></td><td>Imports CSV file to be read in PS</td></tr><tr><td><mark style="color:yellow;"><code>Import-Csv C:\path\to\file.csv | Format-Table -AutoSize</code></mark></td><td>Formats a CSV file as a table with column width adjusted automatically.</td></tr></tbody></table>
