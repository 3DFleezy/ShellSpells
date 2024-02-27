# Modify

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ipconfig /flushdns</code></mark></td><td>Purge DNS Resolver Cache</td></tr><tr><td><mark style="color:yellow;"><code>arp -d 192.168.0.1</code></mark></td><td>Remove ARP mappings for 192.168.0.1 + on all interfaces.</td></tr><tr><td><mark style="color:yellow;"><code>nbtstat -RR</code></mark></td><td>(Flush NetBIOS Cache) Sends Name Release packets to WINS and starts Refresh</td></tr></tbody></table>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>netsh interface ip set</code></mark></td><td>Sets IP and default gateway for specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ipv4 set</code></mark></td><td>Sets IP and default gateway for specified IPv4 interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ipv6 set</code></mark></td><td>Sets IP and default gateway for specified IPv6 interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ip set dnsservers</code></mark></td><td>Sets DNS servers for specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ipv4 set dnsservers</code></mark></td><td>Sets IPv4 DNS servers for specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ipv6 set dnsservers</code></mark></td><td>Sets IPv6 DNS servers for specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh wlan set hostednetwork</code></mark></td><td>Sets Hosted network settings.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ip add</code></mark></td><td>Adds IP to specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ipv4 add</code></mark></td><td>Adds IPv4 to specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ipv6 add</code></mark></td><td>Adds IPv6 to specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ip delete</code></mark></td><td>Deletes IP from specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ipv4 delete</code></mark></td><td>Deletes IPv4 from specified interface.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ipv6 delete</code></mark></td><td>Deletes IPv6 from specified interface.</td></tr></tbody></table>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Set-NetIPAddress</code></mark></td><td>Modifies IP config properties.</td></tr><tr><td><mark style="color:yellow;"><code>Set-NetAdapter</code></mark></td><td>Modifies basic network interface properties.</td></tr><tr><td><mark style="color:yellow;"><code>New-NetIPAddress</code></mark></td><td>Adds IP to network interface.</td></tr><tr><td><mark style="color:yellow;"><code>Remove-NetIPAddress</code></mark></td><td>Removes IP from network interface.</td></tr><tr><td><mark style="color:yellow;"><code>Set-DnsClientServerAddress</code></mark></td><td>Sets DNS servers for interface.</td></tr></tbody></table>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>Enable-NetAdapter</code></mark></td><td>Enables a network interface.</td></tr><tr><td><mark style="color:yellow;"><code>Disable-NetAdapter</code></mark></td><td>Disables a network interface.</td></tr></tbody></table>



Enables static IP for network interface:

```powershell
wmic nicconfig where "IPEnabled = true" call EnableStatic
```

Enables DHCP on network interface:

```powershell
wmic nicconfig where "IPEnabled = true" call EnableDHCP
```

Sets DNS server search order for network interface:

```powershell
wmic nicconfig where "IPEnabled = true" call SetDNSServerSearchOrder
```

Removes static DNS entry of 192.168.118.1 on the local interface:

```powershell
netsh interface ip delete dns local 192.168.118.1
```

Set static IP Address; Subnet; Gateway; GatewayMetric:

```powershell
netsh interface ip set address local static 192.168.18.111 255.255.255.0 192.168.18.254 1
```

Set a static DNS for local interface:

```powershell
netsh interface ip set dns name=local source=static addr=192.168.118.101
```

## <mark style="color:red;">Registry Locations</mark>

### <mark style="color:purple;">Network Profile Registry Values</mark>

Queries current network profiles:

```powershell
Get-ChildItem 'HKLM:\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\NetworkList\\Profiles'
```

| Network Location Category | Data Value |
| ------------------------- | ---------- |
| Public                    | 0 (ZERO)   |
| Private                   | 1          |
| Domain                    | 2          |

### <mark style="color:purple;">All</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</mark>

This key contains a variety of settings that affect the TCP/IP protocol, including DNS, IP, and WINS settings.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces{Interface GUID}</mark>

Contains settings specific to each network interface, such as IP address, subnet mask, and DNS server addresses.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\NetBT\Parameters</mark>

Settings for NetBIOS over TCP/IP (NetBT) configuration.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient</mark>

Contains DNS client configuration settings, often used in Group Policy settings.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters</mark>

Similar to the Tcpip\Parameters key, but specifically for IPv6 configuration.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkCards</mark>

Information about each network card installed on the system.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings</mark>

Contains settings related to Internet Explorer and overall internet connectivity settings, including proxy settings.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp</mark>

Contains settings for the Remote Desktop Protocol (RDP), including port configuration.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy</mark>

Configuration settings for the Windows Firewall.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Rpc\Internet</mark>

Contains settings for configuring RPC over Internet ports.
