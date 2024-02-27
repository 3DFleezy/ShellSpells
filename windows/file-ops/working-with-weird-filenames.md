# Working With Weird Filenames

## Files with "--"

Use the <mark style="color:yellow;">`.\`</mark> prefix for relative paths or specify the full path.

For cmdlets, you might also use the <mark style="color:yellow;">`--%`</mark> operator, which signals PowerShell to stop parsing the command line, passing the rest of the command directly to a native command.

```powershell
Get-Content .\--weirdfilename.txt
```

```powershell
Remove-Item --% --weirdfilename.txt
```

## Leading or Trailing Spaces

Enclose the filename in quotes and use the backtick (<mark style="color:yellow;">\`</mark>) as the escape character for trailing spaces in PowerShell.

```powershell
Get-Content "filenameWithTrailingSpace `.txt"
```

```powershell
Remove-Item "filenameWithTrailingSpace `.txt"
```

## Wildcard Characters (\*, ?)

Directly use them in quotes if they are part of the filename.

```powershell
Get-Content "file*.txt"
```

```powershell
Remove-Item 'file?.txt'
```
