# Sort

Sorts by the "CPU" property:

```powershell
Get-Process | Sort-Object -Property CPU
```

Sorts by the "CPU" property, and if two are the same, it sorts by the ID, in descending order:

```powershell
Get-Process | Sort-Object CPU,ID -desc
```

Sort files in current dir by creation time:

```powershell
gci | Select Name,CreationTime | Sort-Object CreationTime -desc
```

Sorts the lines in a text file and outputs to another file:

```powershell
sort C:\path\to\file.txt > C:\path\to\sortedfile.txt 
```

Sorts the content of a file alphabetically and saves the sorted content to a new file:

```powershell
type C:\path\to\file.txt | sort > C:\path\to\sortedfile.txt
```
