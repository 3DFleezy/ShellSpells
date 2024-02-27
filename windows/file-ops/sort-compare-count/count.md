# Count

Used to count and can do more:

```powershell
Measure-Object
```

Print only the count of files in the current dir:

```powershell
write-host (Get-ChildItem | Measure-Object).count
```

Count unique entries in a file:

```powershell
Get-Content .\testing.txt | Sort-Object -Unique | Measure-Object
```

Find the 161st word in a file. (Remember: Starts at '0'):

```powershell
((Get-Content .\Word_File.txt).split(" "))[160]
```
