# Attributes

| <mark style="color:yellow;">`dir <path> /a:h /s`</mark> | Hidden files    |
| ------------------------------------------------------- | --------------- |
| <mark style="color:yellow;">`dir <path> /a:s /s`</mark> | System files    |
| <mark style="color:yellow;">`dir <path> /a:r /s`</mark> | Read-only files |
| <mark style="color:yellow;">`dir <path> /a:a /s`</mark> | Any attribute   |

Lists files with the specified attributes in the given path:

```powershell
Get-ChildItem -Path <path> -Attributes <attributes> -Recurse
```

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path <Path> -File -Recurse | Where-Object { $_.Attributes -match "Attribute" }
```
{% endcode %}

Attribute values:

<mark style="color:orange;">Hidden</mark>

<mark style="color:orange;">System</mark>

<mark style="color:orange;">ReadOnly</mark>

<mark style="color:orange;">Archive</mark>

```powershell
wmic datafile where Attributes='<attributes>' get Name, FileName
```

Attribute values:

<mark style="color:yellow;">`h`</mark> (hidden)

<mark style="color:yellow;">`s`</mark> (system)

<mark style="color:yellow;">`r`</mark> (read-only)

<mark style="color:yellow;">`a`</mark> (archive)

Combine attributes using a plus sign (+), e.g., /a:h+s for hidden and system files.
