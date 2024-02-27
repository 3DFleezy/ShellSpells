# Enumerate

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ipconfig</code></mark></td><td>TCP/IP network config.</td></tr><tr><td><mark style="color:yellow;"><code>ipconfig /all</code></mark></td><td>TCP/IP config for all adapters.</td></tr><tr><td><mark style="color:yellow;"><code>ipconfig /displaydns</code></mark></td><td>DNS Resolver Cache.</td></tr><tr><td><mark style="color:yellow;"><code>netstat</code></mark></td><td>Stats and port info.</td></tr><tr><td><mark style="color:yellow;"><code>netstat -a</code></mark></td><td>Active TCP and UDP ports.</td></tr><tr><td><mark style="color:yellow;"><code>netstat -n</code></mark></td><td>Active TCP connections, numeric addresses and ports.</td></tr><tr><td><mark style="color:yellow;"><code>netstat -o</code></mark></td><td>Active TCP connections with PIDs.</td></tr><tr><td><mark style="color:yellow;"><code>netstat -b</code></mark></td><td>Executables for each connection.</td></tr><tr><td><mark style="color:yellow;"><code>nbtstat -rn</code></mark></td><td>NetBIOS info.</td></tr><tr><td><mark style="color:yellow;"><code>nbtstat -a [RemoteName]</code></mark></td><td>Remote machine name table given its NAME.</td></tr><tr><td><mark style="color:yellow;"><code>nbtstat -A [IP address]</code></mark></td><td>Remote machine name table given its IP.</td></tr><tr><td><mark style="color:yellow;"><code>route print</code></mark></td><td>Routing tables.</td></tr><tr><td><mark style="color:yellow;"><code>fport</code></mark></td><td>TCP/IP process to port mapper.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ?</code></mark></td><td>Help.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface show interface</code></mark></td><td>All network interfaces.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ip show address</code></mark></td><td>IP; DHCP; Subnet; Gateway.</td></tr><tr><td><mark style="color:yellow;"><code>netsh interface ip show config</code></mark></td><td>TCP/IP network config values.</td></tr><tr><td><mark style="color:yellow;"><code>netsh wlan show interfaces</code></mark></td><td>Wireless network interface info.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetIPConfiguration</code></mark></td><td>Config for all interfaces.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetAdapter | Get-NetIPAddress</code></mark></td><td>IPs and DHCP config for all network adapters.</td></tr><tr><td><mark style="color:yellow;"><code>Test-NetConnection</code></mark></td><td>Diagnostic info for a connection.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetIPAddress</code></mark></td><td>IP config.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetAdapter</code></mark></td><td>Basic network adapter properties.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetAdapterBinding</code></mark></td><td>Network adapter binding settings.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetAdapterStatistics</code></mark></td><td>Network adapter statistics.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetRoute</code></mark></td><td>IP routing table.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetTCPConnection</code></mark></td><td>TCP connections.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetUDPEndpoint</code></mark></td><td>Retrieves UDP listener endpoints.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetUDPSetting</code></mark></td><td>Global UDP settings.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetTCPSetting</code></mark></td><td>Global TCP settings.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetIPConfiguration -InterfaceIndex 4</code></mark></td><td>Check interface by index.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetIPInterface -InterfaceAlias "Wi-Fi"</code></mark></td><td>Check interface by name.</td></tr><tr><td><mark style="color:yellow;"><code>wmic netuse list brief</code></mark></td><td>Active connections info (Brief).</td></tr><tr><td><mark style="color:yellow;"><code>wmic netuse list full</code></mark></td><td>Active connections info (Full).</td></tr><tr><td><mark style="color:yellow;"><code>wmic netuse get name, connectionstate, username</code></mark></td><td>Active connections specific properties.</td></tr><tr><td><mark style="color:yellow;"><code>wmic nicconfig get</code></mark></td><td>Network adapter configs.</td></tr><tr><td><mark style="color:yellow;"><code>wmic nic get NetConnectionStatus</code></mark></td><td>Network interfaces and their connection status.</td></tr><tr><td><mark style="color:yellow;"><code>wmic netuse get name,status</code></mark></td><td>Network resources connected to the system.</td></tr><tr><td><mark style="color:yellow;"><code>net view</code></mark></td><td>ServerName and Remarks of hosts in current domain.</td></tr><tr><td><mark style="color:yellow;"><code>net view /domain</code></mark></td><td>Hosts on the domain.</td></tr><tr><td><mark style="color:yellow;"><code>nltest /dclist:&#x3C;DOMAIN></code></mark></td><td>DCs.</td></tr><tr><td><mark style="color:yellow;"><code>dsquery computer</code></mark></td><td>Host on the domain.</td></tr></tbody></table>



All hosts:

```powershell
wmic /NAMESPACE:\\root\directory\ldap PATH ds_computer GET ds_samaccountname
```

All hosts:

```powershell
wmic /NAMESPACE:\\root\directory\ldap PATH ds_computer GET ds_dnshostname
```

Retrieves network adapter configuration:

```powershell
Get-CimInstance -ClassName Win32_NetworkAdapterConfiguration
```

Retrieves properties of a network adapter:

```powershell
Get-CimInstance -ClassName Win32_NetworkAdapter
```

Lists TCP/IP printer ports:

```powershell
Get-CimInstance -ClassName Win32_TCPIPPrinterPort
```

Performance data from network interfaces:

```powershell
Get-CimInstance -ClassName Win32_PerfFormattedData_Tcpip_NetworkInterface
```

Performance data from IPv4 TCP/IP protocol:

```powershell
Get-CimInstance -ClassName Win32_PerfFormattedData_Tcpip_TCPv4
```

Performance data from IPv6 TCP/IP protocol:

```powershell
Get-CimInstance -ClassName Win32_PerfFormattedData_Tcpip_TCPv6
```

## <mark style="color:red;">DHCP</mark>

```powershell
ipconfig /all
```

```powershell
reg query HKLM\SYSTEM\CurrentControlSet\Services\ /s /v "EnableDHCP"
```

```powershell
Get-Service dhcp
```

```powershell
netsh interface ip show config
```

```powershell
Get-NetIPConfiguration
```

### <mark style="color:purple;">Graphical User Interface (GUI):</mark>

Network and Sharing Center

Open the Control Panel.

Go to "Network and Internet" > "Network and Sharing Center."

Click on "Change adapter settings."

Right-click on the network adapter you want to check and select "Properties."

Double-click on "Internet Protocol Version 4 (TCP/IPv4)."

If "Obtain an IP address automatically" is selected, DHCP is enabled.

## <mark style="color:red;">DNS</mark>

C:\Windows\System32\Drivers\etc\hosts

This file is how DNS worked before DNS. You can set domain names to incorrect IPs.

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>netsh interface ip show dns</code></mark></td><td>Display DNS information on network interface.</td></tr><tr><td><mark style="color:yellow;"><code>ipconfig /all</code></mark></td><td>Look for the "DNS Servers" line under each adapter's section. If DNS is enabled and configured, you'll see IP addresses listed there.</td></tr><tr><td><mark style="color:yellow;"><code>nslookup</code></mark></td><td>If DNS is working correctly, you should be able to type nslookup followed by a domain name (e.g., nslookup google.com) and get an IP address response.</td></tr><tr><td><mark style="color:yellow;"><code>Get-DnsClientServerAddress</code></mark></td><td>Retrieves the DNS server addresses configured for each network interface. An empty list indicates that DNS is disabled.</td></tr><tr><td><mark style="color:yellow;"><code>Resolve-DnsName google.com</code></mark></td><td>Performs a DNS lookup and displays results, indicating DNS functionality.</td></tr><tr><td><mark style="color:yellow;"><code>Test-Connection -ComputerName google.com -DnsOnly</code></mark></td><td>Tests DNS resolution specifically. If successful, DNS is enabled.</td></tr><tr><td><mark style="color:yellow;"><code>Get-DnsClientServerAddress -InterfaceAlias "Wi-Fi"</code></mark></td><td>Target specific interfaces.</td></tr><tr><td><mark style="color:yellow;"><code>Resolve-DnsName -InterfaceAlias "Ethernet" google.com</code></mark></td><td>Target specific interfaces.</td></tr></tbody></table>

### <mark style="color:purple;">Graphical User Interface (GUI):</mark>

Network and Sharing Center:

Open the Control Panel.

Go to "Network and Internet" > "Network and Sharing Center."

Click on "Change adapter settings."

Right-click on the network adapter you want to check and select "Properties."

Double-click on "Internet Protocol Version 4 (TCP/IPv4)."

If DNS server addresses are manually entered or obtained automatically, DNS is enabled.

## <mark style="color:red;">ARP</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="407">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>arp -a</code></mark></td><td>Displays current ARP entries.</td></tr><tr><td><mark style="color:yellow;"><code>arp -a inet_address</code></mark></td><td>Displays current ARP entries for <mark style="color:yellow;"><code>inet_address</code></mark>only.</td></tr><tr><td><mark style="color:yellow;"><code>Get-NetNeighbor -AddressFamily IPv4</code></mark></td><td>If ARP is working, you'll see entries mapping IP addresses to MAC addresses. An empty cache might indicate ARP issues, but it's not conclusive.</td></tr><tr><td><mark style="color:yellow;"><code>ping &#x3C;IP></code></mark></td><td>Test ARP. If successful, ARP is likely enabled. If ARP fails, ping won't succeed.</td></tr></tbody></table>

### <mark style="color:purple;">GUI: Inspect Network Adapter Properties:</mark>

Control Panel > Network and Internet > Network and Sharing Center > Change adapter settings

Right-click adapter > Properties > Configure > Advanced

Look for settings related to ARP:

Might include enabling/disabling ARP or adjusting cache size.

If ARP options are present and not disabled, it's likely enabled.

## <mark style="color:red;">Port Status</mark>

<table data-full-width="true"><thead><tr><th width="192">State</th><th>Description</th></tr></thead><tbody><tr><td>CLOSED</td><td>Indicates that the server has received an ACK signal (to acknowledge receipt of a packet) from the client and the connection is closed.</td></tr><tr><td>CLOSE_WAIT</td><td>Indicates that the server has received the first FIN signal (to acknowledge there is no more data to be sent) from the client and the connection is in the process of closing.</td></tr><tr><td>ESTABLISHED</td><td>Indicates that the server received the SYN signal (synchronize, this signal is only sent in the first packet) from the client and the session is established.</td></tr><tr><td>FIN_WAIT_1</td><td>Indicates that the connection is still active but not currently being used.</td></tr><tr><td>FIN_WAIT_2</td><td>Indicates that the client just received acknowledgment of the first FIN signal from the server.</td></tr><tr><td>LAST_ACK</td><td>Indicates that the server is in the process of sending its own FIN signal.</td></tr><tr><td>LISTENING</td><td>Indicates that the server is ready to accept a connection.</td></tr><tr><td>SYN_RECEIVED</td><td>Indicates that the server just received a SYN signal from the client.</td></tr><tr><td>SYN_SEND</td><td>Indicates that this connection is open and active.</td></tr><tr><td>TIME_WAIT</td><td>Indicates that the client recognizes the connection as active, but not currently being used.</td></tr></tbody></table>
