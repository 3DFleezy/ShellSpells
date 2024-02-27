# Move

Move file (mv, move, mi)

```powershell
Move-Item src.txt dst.txt
```

Move file:

```powershell
move src.txt dst.txt
```

Renames (effectively moves) a file within the same directory.

Not applicable for moving to different directories.

```powershell
ren C:\source\file.txt C:\destination\file.txt
```

Uses Robocopy to move a file by copying it to the destination and then deleting it from the source.

```powershell
robocopy C:\source C:\destination file.txt /MOV
```

Moves a file using .NET's System.IO.File class in a PowerShell script.

```powershell
[System.IO.File]::Move("C:\source\file.txt", "C:\destination\file.txt")
```

Moves a file by copying it with attributes and then deleting the source file.

Note: This is technically a copy operation followed by a delete, but achieves the move effect.

{% code overflow="wrap" %}
```powershell
xcopy C:\source\file.txt C:\destination\file.txt /O /X /Y /H /K && del C:\source\file.txt
```
{% endcode %}
