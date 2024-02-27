# Modify

<table data-header-hidden data-full-width="true"><thead><tr><th width="539">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>New-Item -Path Registry::HKLM\Software\MyKey</code></mark></td><td>Create registry key</td></tr><tr><td><mark style="color:yellow;"><code>reg add HKLM\Software\MyKey /v MyValue /t REG_SZ /d "Data"</code></mark></td><td>Add registry key</td></tr><tr><td><mark style="color:yellow;"><code>Set-ItemProperty -Path Registry::HKLM\Software\MyKey -Name &#x3C;Name> -Value "Data"</code></mark></td><td>Set key value</td></tr><tr><td><mark style="color:yellow;"><code>Set-ItemProperty -Path dwm -PSProperty EnableAeroPeek -Value 0</code></mark></td><td>Set EnableAeroPeek to 0</td></tr><tr><td><mark style="color:yellow;"><code>reg delete HKLM\Software\MyKey /v MyValue</code></mark></td><td>Delete registry key or value</td></tr><tr><td><mark style="color:yellow;"><code>Remove-Item -Path Registry::HKLM\Software\MyKey</code></mark></td><td>Delete registry key and its subkeys in PowerShell</td></tr><tr><td><mark style="color:yellow;"><code>Remove-ItemProperty -Path Registry::HKLM\Software\MyKey -Name MyValue</code></mark></td><td>Delete registry value</td></tr><tr><td><mark style="color:yellow;"><code>reg copy HKLM\Software\MyKey HKLM\Software\NewKey</code></mark></td><td>Copy registry key and its subkeys to a new location</td></tr><tr><td><mark style="color:yellow;"><code>reg import filename.reg</code></mark></td><td>Imports registry settings</td></tr><tr><td><mark style="color:yellow;"><code>reg export HKLM\Software\MyKey filename.reg</code></mark></td><td>Exports registry key and its subkeys</td></tr><tr><td><mark style="color:yellow;"><code>reg save HKLM\Software\MyKey filename.hiv</code></mark></td><td>Saves a registry key and its subkeys in Hive (HIV) format</td></tr><tr><td><mark style="color:yellow;"><code>reg load HKLM\TempKey filename.hiv</code></mark></td><td>Loads a Hive (HIV) file into the registry</td></tr><tr><td><mark style="color:yellow;"><code>reg unload HKLM\TempKey</code></mark></td><td>Unloads a previously loaded Hive (HIV) file from the registry</td></tr></tbody></table>

Create the value Test in the RunOnce subkey of HKLM using the following command:

{% code overflow="wrap" %}
```powershell
reg add hklm\software\microsoft\windows\currentversion\runonce /v Test /t REG_BINARY /d 1111
```
{% endcode %}

Modify the binary value of Test using the following command:

{% code overflow="wrap" %}
```powershell
reg add hklm\software\microsoft\windows\currentversion\runonce /v Test /t REG_BINARY /d 1111
```
{% endcode %}

Delete the binary value for Test using the following command:

{% code overflow="wrap" %}
```powershell
reg delete hklm\software\microsoft\windows\currentversion\runonce /v Test
```
{% endcode %}
