# One Liners

Extensive info about a specified file (Must use full path, must use double backspaces):

{% code overflow="wrap" %}
```powershell
wmic datafile where name='C:\\Users\\STUFF.txt' get Archive, Compressed, CreationDate, Description, Drive, Encrypted, Extension, FileName, FileType, FSName, Hidden, InstallDate, InUseCount, LastAccessed, LastModified, Manufacturer, Name, Path, Readable, Size, Status, System, Version /format:list
```
{% endcode %}
