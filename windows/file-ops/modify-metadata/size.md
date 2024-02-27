# Size

Creates a file using zeroes to meet the specified size.

The file content will be empty, however:

```powershell
fsutil file createnew <filename> <size in bytes>
```

If you add content to the file, the size will increase from the specified size.

If you overwrite the file, it will reset the size.

Example:

```powershell
fsutil file createnew test.txt 55
```

test.txt is 55 bytes, but there is no content.

```powershell
echo thisthat >> test.txt
```

test.txt is now 66 bytes

```powershell
echo thisthat > test.txt
```

test.txt is now 11 bytes because it was completely overwritten.
