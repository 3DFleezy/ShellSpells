# Attributes

## Commands

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>attrib &#x3C;file></code></mark></td><td>Displays file attributes</td></tr><tr><td><mark style="color:yellow;"><code>Get-Item &#x3C;file> | Select-Object Attributes</code></mark></td><td>Displays file attributes</td></tr></tbody></table>

All files in dir:

{% code overflow="wrap" %}
```powershell
Get-ChildItem <Path> | ForEach-Object { $_.Name + ": " + $_.Attributes.ToString() }
```
{% endcode %}

## File Attributes Explained

<mark style="color:orange;">R</mark> = Read-only. Cannot be written to or deleted.

<mark style="color:orange;">A</mark> = Archive. Marked for backup or removal.

<mark style="color:orange;">S</mark> = System. Used by the system and is not typically displayed in a directory listing.

<mark style="color:orange;">H</mark> = Hidden. Not displayed in a normal directory listing.

<mark style="color:orange;">I</mark> = Not content indexed file.

<mark style="color:orange;">L</mark> = Symbolic link or shortcut.

<mark style="color:orange;">O</mark> = Offline. The file data is not immediately available.

<mark style="color:orange;">P</mark> = Sparse file.

<mark style="color:orange;">T</mark> = Temporary. The file is being used for temporary storage.
