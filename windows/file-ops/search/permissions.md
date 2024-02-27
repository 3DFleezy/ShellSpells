# Permissions

Lists files with specific permissions for a user, recursively:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <path> -Recurse -File | Where-Object { $_.GetAccessControl().Access.IdentityReference -like "<username>*" } | Select-Object FullName
```
{% endcode %}

Lists files with Full Control permissions for a specific user, recursively:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <path> -Recurse -File | Where-Object { $_.GetAccessControl().Access | Where-Object { $_.FileSystemRights -eq "FullControl" -and $_.IdentityReference -like "<username>*" } } | Select-Object FullName
```
{% endcode %}

Lists files with Modify permissions for a specific user, recursively:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <path> -Recurse -File | Where-Object { $_.GetAccessControl().Access | Where-Object { $_.FileSystemRights -eq "Modify" -and $_.IdentityReference -like "<username>*" } } | Select-Object FullName
```
{% endcode %}

Lists files with Read permissions for a specific user, recursively:

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <path> -Recurse -File | Where-Object { $_.GetAccessControl().Access | Where-Object { $_.FileSystemRights -eq "Read" -and $_.IdentityReference -like "<username>*" } } | Select-Object FullName
```
{% endcode %}

Filtering Files Based on Specific Permissions:

{% code overflow="wrap" %}
```
Get-ChildItem -Path "C:\Folder" -Recurse -File | Where-Object {
    $_.GetAccessControl().Access | Where-Object {
        $_.FileSystemRights -eq "FullControl" -and $_.IdentityReference -like "BUILTIN\Administrators"
    }
} | Select-Object FullName
```
{% endcode %}

Checking for Write Permission for a Group:

{% code overflow="wrap" %}
```
$acl = Get-Acl -Path "C:\TestFolder"
$hasWriteAccess = $acl.Access | Where-Object {
    $_.IdentityReference -like "DOMAIN\MyGroup*" -and $_.FileSystemRights -band [System.Security.AccessControl.FileSystemRights]::Write
}
if ($hasWriteAccess) {
    Write-Host "The group has Write access."
} else {
    Write-Host "The group does not have Write access."
}
```
{% endcode %}

Combining Multiple Permission Checks:

{% code overflow="wrap" %}
```
Get-ChildItem -Path "C:\ImportantFiles" -Recurse -File | Where-Object {
    $_.GetAccessControl().Access | Where-Object {
        ($_.FileSystemRights -eq "FullControl" -and $_.IdentityReference -like "BUILTIN\Administrators") -or
        ($_.FileSystemRights -band [System.Security.AccessControl.FileSystemRights]::Write -and $_.IdentityReference -like "DOMAIN\Users")
    }
} | Select-Object FullName
```
{% endcode %}

Key Points:

Access the FileSystemRights property to examine permissions granted to a specific user or group.

Use comparison operators (==, -eq) to check for exact permission matches.

Employ the <mark style="color:yellow;">`-band`</mark> operator for bitwise comparison to check for specific permission flags within a set of permissions.

Combine multiple <mark style="color:yellow;">`Where-Object`</mark> clauses for complex permission filtering.

Leverage PowerShell's object manipulation capabilities for advanced permission analysis and management.
