# Size

<table data-header-hidden data-full-width="true"><thead><tr><th width="558">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>dir &#x3C;file></code></mark></td><td>Bytes</td></tr><tr><td><mark style="color:yellow;"><code>Get-ChildItem &#x3C;file> | Select-Object Name, Length</code></mark></td><td>Bytes</td></tr><tr><td><mark style="color:yellow;"><code>wmic datafile where name='C:\\file.txt' get FileSize</code></mark></td><td>Bytes</td></tr></tbody></table>

Convert to KB and rounds to 2 decimal places:

{% code overflow="wrap" %}
```powershell
Get-ChildItem <file> | Select-Object Name, @{Name="Size";Expression={[math]::Round($_.Length / 1KB,2)}}
```
{% endcode %}

Convert to MB and rounds to 2 decimal places:

{% code overflow="wrap" %}
```powershell
Get-ChildItem <file> | Select-Object Name, @{Name="Size";Expression={[math]::Round($_.Length / 1MB,2)}}
```
{% endcode %}

Convert to GB and rounds to 2 decimal places:

{% code overflow="wrap" %}
```powershell
Get-ChildItem <file> | Select-Object Name, @{Name="Size";Expression={[math]::Round($_.Length / 1GB,2)}}
```
{% endcode %}
