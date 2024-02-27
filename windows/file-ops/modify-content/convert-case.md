# Convert Case

Convert the content of a file to uppercase:

{% code overflow="wrap" %}
```powershell
Get-Content C:\path\to\file.txt | ForEach-Object { $_.ToUpper() } | Set-Content C:\path\to\uppercasefile.txt
```
{% endcode %}
