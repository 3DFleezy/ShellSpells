# Antivirus

## <mark style="color:red;">Enumerate</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sc queryex type= service &#x26;#124; find /i "Antivirus"</code></mark></td><td>Lists services related to antivirus.</td></tr><tr><td><mark style="color:yellow;"><code>net start &#x26;#124; find "Antivirus"</code></mark></td><td>Lists started services filtering for "Antivirus".</td></tr><tr><td><mark style="color:yellow;"><code>tasklist &#x26;#124; findstr /i "antivirus"</code></mark></td><td>Lists processes and filters for antivirus.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Service &#x26;#124; Where-Object {$_.DisplayName -like "*antivirus*"}</code></mark></td><td>Filters services with "antivirus" in their name.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Process &#x26;#124; Where-Object {$_.ProcessName -like "*antivirus*"}</code></mark></td><td>Filters processes related to antivirus by name.</td></tr></tbody></table>

Retrieves antivirus name and state:

{% code overflow="wrap" %}
```powershell
wmic /Node:localhost /Namespace:\\root\SecurityCenter2 Path AntiVirusProduct Get displayName,productState /Format:List
```
{% endcode %}

Gets antivirus info via PowerShell and Get-CimInstance:

```powershell
Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntiVirusProduct 
```

Runs PowerShell command in CMD to get antivirus info using Get-WmiObject.

{% code overflow="wrap" %}
```powershell
powershell "Get-WmiObject -Namespace root\SecurityCenter2 -Class AntiVirusProduct"
```
{% endcode %}

Retrieve antivirus product name and state using WMIC from the SecurityCenter2 namespace.

{% code overflow="wrap" %}
```powershell
wmic /Node:localhost /Namespace:\\root\SecurityCenter2 Path AntiVirusProduct Get displayName,productState /Format:List
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
wmic /node:localhost /namespace:\\root\securitycenter2 path antivirusproduct get displayname /format:list
```
{% endcode %}

Lists the antispywareproduct class from the root/security instance (Can't get this to work...):

```powershell
Get-CimInstance -Namespace root\\securitycenter2 -ClassName antispywareproduct
```

## <mark style="color:red;">Registry Location</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall</mark>

Contains information about all installed software, including antivirus applications. Each application has its own subkey with details about the installation.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall</mark>

On 64-bit Windows, this key contains information about 32-bit applications installed on the system, including 32-bit antivirus software.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Security Center\Provider\Av</mark>

Used by older versions of Windows to store information about registered antivirus products.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Security Center\Svc\Providers</mark>

In newer versions of Windows, this key and its subkeys contain information about security providers, including antivirus software.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services</mark>

Holds information about all system services, including those related to antivirus software. Each antivirus service will have a subkey here with configuration details.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Run</mark>

May contain entries for antivirus software that is set to run at startup. This location is often used for applications to configure themselves to start with Windows.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run</mark>

Similar to the HKCU version, this key is used to launch programs automatically at startup, including potentially antivirus software, but applies to all users on the system.
