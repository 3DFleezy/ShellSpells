# Replace / Remove

## Replace Strings

Replaces text with new text and outputs to new file (From CMD terminal):

{% code overflow="wrap" %}
```powershell
type C:\file.txt | powershell -Command "$input | % { $_ -replace 'oldtext', 'newtext' }" > C:\modifiedfile.txt
```
{% endcode %}

Replace a string in the file content

{% code overflow="wrap" %}
```powershell
(Get-Content C:\path\to\file.txt) -replace 'oldString', 'newString' | Set-Content C:\path\to\modifiedfile.txt
```
{% endcode %}

## Remove Strings

## Remove Lines

<table data-header-hidden data-full-width="true"><thead><tr><th width="622">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>type C:\file.txt | findstr /v "pattern" > C:\newfile.txt</code></mark></td><td>Lines without "pattern"</td></tr><tr><td><mark style="color:yellow;"><code>type C:\file.txt | more +10 > C:\trimmedfile.txt</code></mark></td><td>First 10 lines</td></tr><tr><td><mark style="color:yellow;"><code>type C:\file.txt | find /v "" > C:\nonemptyfile.txt</code></mark></td><td>Non-empty lines</td></tr></tbody></table>

## Remove Whitespace

Trim leading and trailing whitespaces from each line:

{% code overflow="wrap" %}
```powershell
Get-Content C:\file.txt | ForEach-Object { $_.Trim() } | Set-Content C:\trimmedfile.txt
```
{% endcode %}
