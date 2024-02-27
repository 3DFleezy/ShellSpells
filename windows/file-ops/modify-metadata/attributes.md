# Attributes

<mark style="color:yellow;">`R`</mark> Read-only

<mark style="color:yellow;">`A`</mark> Archive

<mark style="color:yellow;">`S`</mark> System

<mark style="color:yellow;">`H`</mark> Hidden



| <mark style="color:yellow;">`attrib +R <file>`</mark>    | Add read-only attribute             |
| -------------------------------------------------------- | ----------------------------------- |
| <mark style="color:yellow;">`attrib -H <file>`</mark>    | Remove hidden attribute             |
| <mark style="color:yellow;">`attrib +H +S <file>`</mark> | Set as Hidden and System attributes |
| <mark style="color:yellow;">`attrib +h *.txt`</mark>     | Hide all .txt files                 |

Add read-only:

{% code overflow="wrap" %}
```powershell
Set-ItemProperty <file> -Name Attributes -Value ([System.IO.FileAttributes]::ReadOnly)
```
{% endcode %}

Remove read-only:

{% code overflow="wrap" %}
```powershell
$attributes = (Get-Item <Path\FileName>).Attributes -band (-bnot [System.IO.FileAttributes]::ReadOnly)
```
{% endcode %}

```powershell
Set-ItemProperty <Path\FileName> -Name Attributes -Value $attributes
```

Add multple attributes:

{% code overflow="wrap" %}
```powershell
$attributes = (Get-Item <Path\FileName>).Attributes -bor [System.IO.FileAttributes]::Hidden -bor [System.IO.FileAttributes]::System
```
{% endcode %}

```powershell
Set-ItemProperty <Path\FileName> -Name Attributes -Value $attributes
```
