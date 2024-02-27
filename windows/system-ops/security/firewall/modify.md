# Modify

## <mark style="color:red;">Enable/Disable Firewall</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>netsh firewall reset</code></mark></td><td>Completely removes/resets firewall settings.</td></tr><tr><td><mark style="color:yellow;"><code>netsh firewall set opmode enable</code></mark></td><td>Enables Windows Firewall.</td></tr><tr><td><mark style="color:yellow;"><code>netsh firewall set opmode disable</code></mark></td><td>Disables Windows Firewall.</td></tr><tr><td><mark style="color:yellow;"><code>netsh advfirewall set allprofiles state off</code></mark></td><td>Toggles firewall off for all profiles.</td></tr><tr><td><mark style="color:yellow;"><code>netsh advfirewall set currentprofile state off</code></mark></td><td>Toggles firewall off for the current profile.</td></tr><tr><td><mark style="color:yellow;"><code>Set-NetFirewallProfile -Profile Domain -Enabled True</code></mark></td><td>Toggles firewall for the specified profile (can toggle all at once: Domain, Private, Public).</td></tr><tr><td><mark style="color:yellow;"><code>netsh advfirewall set privateprofile state on</code></mark></td><td>Toggles firewall on for the specified profile.</td></tr></tbody></table>

## <mark style="color:red;">Logging</mark>

Log dropped connections on all profiles:

```powershell
netsh advfirewall set allprofiles logging droppedconnections enable
```

Log dropped packets and connections:

```powershell
netsh firewall set logging droppedpackets=enable connections=enable
```

Set current profile log's max size:

```powershell
netsh advfirewall set currentprofile logging maxfilesize 1024
```

## <mark style="color:red;">Add Rules</mark>

```powershell
New-NetFirewallRule
```

{% code overflow="wrap" %}
```powershell
New-NetFirewallRule -DisplayName "<RuleName>" -Direction Inbound -Program "c:\my.exe" -Action Allow
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
New-NetFirewallRule -DisplayName "<RuleName>" -Direction Outbound -Program "c:\my.exe" -Action Block
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
New-NetFirewallRule -DisplayName <RuleName> RemoteAddress 10.10.10.25 -Action Allow
```
{% endcode %}

```powershell
netsh advfirewall firewall add rule
```

{% code overflow="wrap" %}
```powershell
netsh advfirewall firewall add rule name="<RuleName>" dir=out action=block program="c:\my.exe" enable=yes
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
netsh advfirewall firewall add rule name="<RuleName>" dir=in action=allow program="c:\my.exe" enable=yes
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
netsh advfirewall firewall add rule name="<RuleName>" dir=in protocol=tcp localport=443 profile=public action=allow
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
netsh advfirewall firewall add rule name="<RuleName>" dir=in protocol=udp localport=443 profile=public action=allow
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
netsh advfirewall firewall add rule name="<RuleName>" dir=in action=allow protocol=TCP localport=443 
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
netsh advfirewall firewall add rule name="<RuleName>" dir=in action=allow program="c:\my.exe" profile=private enable=yes
```
{% endcode %}

{% code overflow="wrap" %}
```powershell
netsh advfirewall firewall add rule name="<RuleName>" dir=in action=allow protocol=tcp localport=31337 remoteport=6666 remoteip=192.168.11.14 profile=private 
```
{% endcode %}

## <mark style="color:red;">Delete Rules</mark>

Removes a firewall rule:

```powershell
Remove-NetFirewallRule
```

Removes a firewall rule by name:

```powershell
Remove-NetFirewallRule -DisplayName "<RuleName>"
```

Deletes an existing inbound or outbound firewall rule:

```powershell
netsh advfirewall firewall delete rule
```

Deletes a rule by name:

```powershell
netsh advfirewall delete rule name="<RuleName>"
```

Deletes a rule by name:

```powershell
netsh advfirewall firewall delete rule name="<RuleName>"
```

## <mark style="color:red;">Modify Existing Rules</mark>

Modifies existing firewall rules:

```powershell
Set-NetFirewallRule
```

Enable All ICMP Traffic:

```powershell
netsh firewall set icmpsetting type=all mode=enable
```

Allow inbound echo request:

```powershell
netsh firewall set icmpsetting type=8 mode=enable
```

Disable groups of rules:

```powershell
netsh advfirewall firewall set rule group="<GroupName>" new enable=no
```

Enable groups of rules:

```powershell
netsh advfirewall firewall set rule group="<GroupName>" new enable=yes
```

## <mark style="color:red;">Export/Import Rules</mark>

Create a BACKUP of the netsh firewall configuration:

```powershell
netsh advfirewall export "c:\\FW-Before-Changes.wfw"
```

Restore netsh firewall configuration from BACKUP:

```powershell
netsh advfirewall import "c:\\FW-Before-Changes.wfw"
```

## <mark style="color:red;">Registry Locations</mark>

Globally Open Ports:

{% code overflow="wrap" %}
```powershell
reg query hklm\\system\\currentcontrolset\\services\\sharedaccess\\parameters\\firewallpolicy\\standardprofile\\globallyopenports\\list
```
{% endcode %}

Authorized Apps:

{% code overflow="wrap" %}
```powershell
reg query hklm\\system\\currentcontrolset\\services\\sharedaccess\\parameters\\firewallpolicy\\standardprofile\\authorizedapplications\\list
```
{% endcode %}

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy</mark>

Holds settings for Windows Firewall policies, including rules and profiles for Domain, Private, and Public networks.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Policies\Microsoft\WindowsFirewall</mark>

Contains Windows Firewall configuration settings applied through Group Policy for Domain, Private, and Public profiles.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\WindowsFirewall</mark>

Used by older versions of Windows to store Windows Firewall settings that are applied across different profiles.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Policies\Microsoft\WindowsFirewall</mark>

Stores user-specific Windows Firewall settings applied through Group Policy, affecting the firewall behavior for the current user.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\SharedAccess\Defaults\FirewallPolicy</mark>

Default configuration settings for Windows Firewall, including default rules and policy settings for all profiles.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles</mark>

Contains information on network profiles, which can influence Windows Firewall behavior based on the network's classification (Private, Public, Domain).

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\WindowsFirewall\AdvancedSecurity</mark>

Stores advanced settings for Windows Firewall with Advanced Security, including inbound and outbound rules, and connection security rules.
