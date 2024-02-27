# Modify

## Enable/Disable Remoting

<table data-header-hidden data-full-width="true"><thead><tr><th width="337">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Enable-PSRemoting -Force</code></mark></td><td>Enables PowerShell remoting on the computer, configuring it to receive remote commands securely.</td></tr><tr><td><mark style="color:yellow;"><code>Disable-PSRemoting -Force</code></mark></td><td>Disables PowerShell remoting, preventing the computer from receiving remote commands.</td></tr><tr><td><mark style="color:yellow;"><code>Set-WSManQuickConfig -Force</code></mark></td><td>Configures the computer to use Windows Remote Management (WinRM) with default settings, including security settings.</td></tr></tbody></table>

## Security Descriptor

Modifies the security descriptor of the default PowerShell session configuration, launching a UI to edit permissions.

```powershell
Set-PSSessionConfiguration -Name Microsoft.PowerShell -ShowSecurityDescriptorUI
```

## Authentication

Enables Basic authentication for the WinRM service.

```powershell
winrm set winrm/config/service/Auth '@{Basic="true"}'
```

Enables Credential Security Support Provider (CredSSP) authentication for the WinRM client.

```powershell
winrm set winrm/config/client/Auth '@{CredSSP="true"}'
```

## Encrypted Traffic

Disables the allowance of unencrypted traffic for the WinRM service using PowerShell.

```powershell
Set-Item -Path WSMan:\localhost\Service\AllowUnencrypted -Value $false
```

Toggle unencrypted communication for WinRM service and WinRM client, enforcing encrypted traffic:

{% code overflow="wrap" %}
```powershell
Set-WSManInstance -ResourceURI winrm/config/service -ValueSet @{AllowUnencrypted="false"}
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
Set-WSManInstance -ResourceURI winrm/config/client -ValueSet @{AllowUnencrypted="false"}
```
{% endcode %}

Disables unencrypted traffic for WinRM at the registry level, enhancing security:

{% code overflow="wrap" %}
```powershell
Set-ItemProperty HKLM:\Software\Policies\Microsoft\Windows\WinRM\Service -Name AllowUnencryptedTraffic -Value 0
```
{% endcode %}

## Firewall

Creates a new firewall rule to allow inbound connections on port 5986 for WinRM over HTTPS, increasing security:

{% code overflow="wrap" %}
```powershell
New-NetFirewallRule -DisplayName "WinRM HTTPS" -Direction Inbound -LocalPort 5986 -Protocol TCP -Action Allow
```
{% endcode %}

Removes firewall rules for WinRM HTTP traffic, enhancing security by disallowing unencrypted remote management traffic.

```powershell
Remove-NetFirewallRule -DisplayName "Windows Remote Management (HTTP-In)"
```

Enables the firewall rule for inbound RDP connections, controlling access security:

{% code overflow="wrap" %}
```powershell
Set-NetFirewallRule -DisplayName "Remote Desktop - User Mode (TCP-In)" -Enabled True
```
{% endcode %}

## TrustedHosts

Adding a single item to TrustedHosts:

```powershell
Set-Item WSMan:\\localhost\\Client\\TrustedHosts -Value "Server01"
```

Adding multiple items:

{% code overflow="wrap" %}
```powershell
Set-Item WSMan:\\localhost\\Client\\TrustedHosts -Value "Server01,Server02,127.0.0.1"
```
{% endcode %}

Appends the Value instead of changing it:

```powershell
Set-Item WSMan:\\localhost\\Client\\TrustedHosts -Value "Server03" -Concatenate
```

Configures the WinRM client to trust specific hosts, enhancing security by limiting remote connections.

```powershell
Set-Item -Path WSMan:\localhost\Client\TrustedHosts -Value "hostname1,hostname2"
```
