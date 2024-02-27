# Users (Owners)

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>dir /q &#x3C;file></code></mark></td><td>Owner</td></tr><tr><td><mark style="color:yellow;"><code>forfiles /S /M "*.*" /C "cmd /c whoami /fo owner %p"</code></mark></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>icacls "C:\Windows\System32\cmd.exe"</code></mark></td><td>Includes owner</td></tr><tr><td><mark style="color:yellow;"><code>Get-Acl</code></mark></td><td>Owner is part of the ACL</td></tr><tr><td><mark style="color:yellow;"><code>Get-Acl &#x3C;Path> | Select-Object -ExpandProperty Owner</code></mark></td><td>Gets the owner of the file or directory at the specified path.</td></tr></tbody></table>



Recursive:

{% code overflow="wrap" %}
```powershell
Get-ChildItem <Path> -Recurse | ForEach-Object { Get-Acl $_.FullName } | Select-Object Path, Owner
```
{% endcode %}

Specific directory:

```powershell
Get-ChildItem <Path> -File | Get-Acl | Select-Object -ExpandProperty Owner
```
