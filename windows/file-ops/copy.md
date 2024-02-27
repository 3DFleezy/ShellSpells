# Copy

## Commands

<table data-header-hidden data-full-width="true"><thead><tr><th width="517">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Copy-Item src.txt dst.txt</code></mark></td><td>Copy a file (cp, copy, cpi)</td></tr><tr><td><mark style="color:yellow;"><code>Copy-Item -Path file.txt -Destination file.txt</code></mark></td><td>Copy</td></tr><tr><td><mark style="color:yellow;"><code>cp C:\source\file.txt C:\destination\file.txt</code></mark></td><td>Alias for Copy-Item</td></tr><tr><td><mark style="color:yellow;"><code>copy C:\source\file.txt C:\destination\file.txt</code></mark></td><td>Copy using CMD.</td></tr><tr><td><mark style="color:yellow;"><code>robocopy C:\source C:\destination file.txt /E</code></mark></td><td>Recursive copy (/E).</td></tr><tr><td><mark style="color:yellow;"><code>type C:\path\to\file.txt | clip</code></mark></td><td>Copies content to clipboard.</td></tr></tbody></table>

Copies files or directory trees to another location, with options for:

copying empty directories (/E)

assuming destination is a directory (/I)

including hidden and system files (/H)

```powershell
xcopy C:\source\file.txt C:\destination\file.txt /E /I /H
```

Copies a file from one location to another using .NET framework in PowerShell, with $true indicating overwrite if the destination file exists.

```powershell
[System.IO.File]::Copy("C:\source\file.txt", "C:\destination\file.txt", $true)
```

Merges the content of two files into a third file.

```powershell
copy C:\path\to\file1.txt + C:\path\to\file2.txt C:\path\to\mergedfile.txt
```

## Clipboard Ops

<table data-header-hidden data-full-width="true"><thead><tr><th width="552">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Get-Clipboard</code></mark></td><td>Get clipboard contents</td></tr><tr><td><mark style="color:yellow;"><code>type C:\path\to\file.txt | clip</code></mark></td><td>Copies file content to clipboard.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Content C:\path\to\file.txt | Set-Clipboard</code></mark></td><td>Copies file content to clipboard.</td></tr><tr><td><mark style="color:yellow;"><code>"Some text" | Set-Clipboard</code></mark></td><td>Copies text to clipboard</td></tr><tr><td><mark style="color:yellow;"><code>Get-ChildItem C:\path\to\directory | Set-Clipboard</code></mark></td><td>Copies file listing to clipboard.</td></tr></tbody></table>

## Copy SAM and System Hive

Backup SAM and SYSTEM hashes:

```
reg save hklm\system C:\system.hive
```

```
reg save hklm\sam C:\sam.hive
```
