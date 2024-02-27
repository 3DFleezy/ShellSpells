# Change Owner

Take ownership of a file:

```powershell
takeown /f <file>
```

Follow these steps in PS:

1. Get a reference to the file:

```powershell
$file = Get-Item <Path\FileName>
```

2. Get the current ACL of the file:

```powershell
$acl = Get-Acl $file.FullName
```

3. Specify the new owner's user account:

```powershell
$user = "DOMAIN\User"
```

4. Create new ACL entry with the new owner:

```powershell
$acl.SetOwner([System.Security.Principal.NTAccount]$user)
```

5. Apply the new ACL to the file:

```powershell
Set-Acl -Path $file.FullName -AclObject $acl 
```
