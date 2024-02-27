# Enumerate

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Get-PSSessionConfiguration</code></mark></td><td>Lists all registered PowerShell session configurations.</td></tr><tr><td><mark style="color:yellow;"><code>winrm get winrm/config</code></mark></td><td>Displays the current WinRM configuration.</td></tr><tr><td><mark style="color:yellow;"><code>winrm get winrm/config/Service</code></mark></td><td>Displays the security configuration for the WinRM service.</td></tr><tr><td><mark style="color:yellow;"><code>winrm get winrm/config/Client</code></mark></td><td>Displays the WinRM client configuration.</td></tr><tr><td><mark style="color:yellow;"><code>Get-WSManInstance winrm/config -Enumerate</code></mark></td><td>Retrieves the current WinRM configuration.</td></tr><tr><td><mark style="color:yellow;"><code>Get-WSManCredSSP</code></mark></td><td>Displays the Credential Security Support Provider (CredSSP) configuration for WinRM, which affects remote authentication.</td></tr><tr><td><mark style="color:yellow;"><code>Get-PSSessionConfiguration | fl *</code></mark></td><td>Lists detailed information about all PowerShell session configurations</td></tr><tr><td><mark style="color:yellow;"><code>Get-Item -Path WSMan:\localhost\Client\TrustedHosts</code></mark></td><td>Lists the hosts trusted by the WinRM client, impacting remote command execution security.</td></tr><tr><td><mark style="color:yellow;"><code>Get-Item -Path WSMan:\localhost\Service\Auth</code></mark></td><td>Shows the authentication methods supported by the WinRM service, indicating security protocols in use.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetFirewallRule -DisplayName "Windows Remote Management (HTTP-In)"</code></mark></td><td>Lists firewall rules for WinRM HTTP traffic, impacting network security for remote management.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetFirewallRule -DisplayName "Remote Desktop - User Mode (TCP-In)"</code></mark></td><td>Lists firewall rules for inbound Remote Desktop Protocol (RDP) connections, affecting RDP security.</td></tr></tbody></table>

Retrieves Remote Desktop Protocol (RDP) security settings using WMI:

{% code overflow="wrap" %}
```powershell
Get-WmiObject -Namespace root\cimv2 -Class Win32_TSGeneralSetting -Filter "TerminalName='RDP-tcp'"
```
{% endcode %}

Retrieves registry settings indicating if unencrypted traffic is allowed for WinRM, affecting security:

{% code overflow="wrap" %}
```powershell
Get-ItemProperty HKLM:\Software\Policies\Microsoft\Windows\WinRM\Service -Name AllowUnencryptedTraffic 
```
{% endcode %}

Queries current network profiles:

{% code overflow="wrap" %}
```powershell
Get-ChildItem 'HKLM:\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\NetworkList\\Profiles'
```
{% endcode %}
