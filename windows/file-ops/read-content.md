# Read Content

## Commands

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>type filename.txt</code></mark></td><td>Displays file content in Command Prompt.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Content filename.txt</code></mark></td><td>Retrieves file content in PowerShell.</td></tr><tr><td><mark style="color:yellow;"><code>gc C:\path\to\file.txt</code></mark></td><td>Another PowerShell alias for Get-Content.</td></tr><tr><td><mark style="color:yellow;"><code>more filename.txt</code></mark></td><td>Shows file content page by page.</td></tr><tr><td><mark style="color:yellow;"><code>notepad filename.txt</code></mark></td><td>Opens file in Notepad.</td></tr><tr><td><mark style="color:yellow;"><code>gc filename.txt</code></mark></td><td>PS alias for <mark style="color:yellow;"><code>Get-Content</code></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>cat C:\path\to\file.txt</code></mark></td><td>PS alias.</td></tr><tr><td><mark style="color:yellow;"><code>notepad C:\path\to\file.txt</code></mark></td><td>Opens a file in Notepad for reading (and editing).</td></tr><tr><td><mark style="color:yellow;"><code>notepad++ C:\path\to\file.txt</code></mark></td><td>Opens a file in Notepad++</td></tr><tr><td><mark style="color:yellow;"><code>[System.IO.File]::ReadAllText("C:\path\to\file.txt")</code></mark></td><td>Reads content using .NET</td></tr></tbody></table>

## Alternate Data Streams

ADS looks like this:

FileName:StreamName:$DATA <-- Normal for files to have $DATA

FileName:StreamName:something <-- Worth investigating

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>dir /R &#x3C;file></code></mark></td><td>Reveal all streams</td></tr><tr><td><mark style="color:yellow;"><code>Get-Item &#x3C;file> -Stream *</code></mark></td><td>Reveal all streams</td></tr><tr><td><mark style="color:yellow;"><code>more &#x3C; &#x3C;file>:&#x3C;streamname></code></mark></td><td>Read specified ADS data</td></tr><tr><td><mark style="color:yellow;"><code>Get-Content &#x3C;file> -Stream &#x3C;streamname></code></mark></td><td>Read specified ADS data</td></tr></tbody></table>
