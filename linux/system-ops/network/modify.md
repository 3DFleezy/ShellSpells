# Modify

## <mark style="color:red;">NICs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="559">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>nmtui</code></td><td>Provides a text user interface to easily modify network interface settings through NetworkManager.</td></tr><tr><td><code>ifconfig &#x3C;interface> &#x3C;IP_address> netmask &#x3C;netmask></code></td><td>Assigns an IP and netmask</td></tr><tr><td><code>ip link set eth0 address 00:11:22:33:44:55</code></td><td>Change MAC address (temporarily)</td></tr><tr><td><code>ifconfig &#x3C;interface> up|down</code> </td><td>Activates/deactivates an interface</td></tr><tr><td><code>ip addr add &#x3C;IP_address>/&#x3C;netmask> dev &#x3C;interface></code></td><td>Adds an IP and netmask</td></tr><tr><td><code>ip addr del &#x3C;IP_address>/&#x3C;netmask> dev &#x3C;interface></code></td><td>Deletes an IP from a network interface</td></tr><tr><td><code>ip link set &#x3C;interface> up|down</code></td><td>Brings a network interface up or down</td></tr><tr><td><code>ip link set dev &#x3C;interface> name &#x3C;new_name></code></td><td>Changes the name of a network interface.</td></tr><tr><td><code>ethtool -G &#x3C;interface> rx &#x3C;value> tx &#x3C;value></code></td><td>Changes the RX and TX ring buffer sizes for an Eth interface.</td></tr><tr><td><code>ethtool -s eth0 speed 100 duplex full autoneg on</code></td><td>Change speed, duplex mode, auto-negotiation</td></tr><tr><td><code>iwconfig &#x3C;interface> essid &#x3C;ESSID></code></td><td>Sets the ESSID (network name) for a wireless network interface.</td></tr><tr><td><code>iwconfig &#x3C;interface> mode &#x3C;mode></code></td><td>Set operating mode of a wireless interface (e.g., Managed, Master, Monitor).</td></tr><tr><td><code>iw &#x3C;interface> set type &#x3C;type></code></td><td>Changes the type of a wireless interface (e.g., managed, monitor) using the <code>iw</code> command.</td></tr><tr><td><code>ip route add|del via dev</code></td><td>Adds or deletes a route to a network or host via a specified gateway</td></tr><tr><td><code>ethtool -s &#x3C;interface> speed &#x3C;speed> duplex &#x3C;duplex> autoneg on|off</code></td><td>Changes the speed, duplex mode, and autonegotiation settings for an Ethernet interface</td></tr><tr><td><code>nmcli device modify &#x3C;interface> ipv4.addresses &#x3C;IP>/&#x3C;netmask> ipv4.gateway &#x3C;gateway> ipv4.dns "&#x3C;dns_servers>"</code></td><td>Modifies the IP address, gateway, and DNS settings for a network interface using NetworkManager</td></tr></tbody></table>

Adds or deletes a route to a network or host via a specified gateway:

```bash
ip route add|del <destination> via <gateway> dev <interface>
```

Changes the speed, duplex mode, and autonegotiation settings for an Ethernet interface:

```bash
ethtool -s <interface> speed <speed> duplex <duplex> autoneg on|off
```

Modifies the IP address, gateway, and DNS settings for a network interface using NetworkManager:

{% code overflow="wrap" %}
```bash
nmcli device modify <interface> ipv4.addresses <IP>/<netmask> ipv4.gateway <gateway> ipv4.dns "<DNS_servers>"
```
{% endcode %}



### <mark style="color:purple;">Config Files (persistent changes)</mark>

Edit /etc/network/interfaces (Debian/Ubuntu):&#x20;

Add lines like `auto eth0`, `iface eth0 inet static`, `address 192.168.1.100`, `netmask 255.255.255.0`.&#x20;

Edit /etc/sysconfig/network-scripts/ifcfg-eth0 (Red Hat/CentOS): \
Modify `BOOTPROTO`, `IPADDR`, `NETMASK`, etc.



## <mark style="color:red;">ARP</mark>

<table data-header-hidden><thead><tr><th width="375">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>arp -d &#x3C;IP></code></td><td>Deletes an ARP</td></tr><tr><td><code>ip neigh del &#x3C;IP></code></td><td>Deletes an ARP</td></tr><tr><td><code>ip neigh del &#x3C;IP_address> dev &#x3C;interface></code></td><td>Deletes an ARP entry for the specified IP</td></tr><tr><td><code>arp -s &#x3C;IP> &#x3C;MAC></code></td><td>Adds a static ARP entry</td></tr><tr><td><code>ip neigh add &#x3C;IP> lladdr &#x3C;MAC></code></td><td>Adds a static ARP entry</td></tr><tr><td><code>ip neigh add &#x3C;IP> lladdr &#x3C;MAC> nud permanent dev &#x3C;interface></code></td><td>Adds a static ARP entry</td></tr></tbody></table>

Replaces or adds an ARP entry. \
If the entry for the specified IP address exists, it is updated; otherwise, a new entry is added:

```bash
ip neigh replace <IP> lladdr <MAC> nud permanent dev <interface>
```

Removes ARP entries matching the `<selector>`, which can be an `IP` , `network`, or `all` to clear the entire ARP cache:&#x20;

```bash
ip neigh flush <selector>
```

## <mark style="color:red;">DNS</mark>

### <mark style="color:purple;">Direct File Editing</mark>

Edit /etc/resolv.conf for temporary changes: \
Add or modify nameserver lines to specify DNS servers. \
Add or modify search lines to set search domains. \
Changes might not persist after network restarts or DHCP updates. \
`sudo vi /etc/resolv.conf`

Modify nsswitch.conf for DNS Lookup Order\
/etc/nsswitch.conf: This file controls the sources from which names are resolved (e.g., hosts, passwords). \
For DNS, you might modify the hosts: line to change the lookup order. \
Example command to edit:\
`sudo vi /etc/nsswitch.conf`

### <mark style="color:purple;">Network Manager (if applicable)</mark>

Use GUI or command-line tools like nmcli or nmtui to modify DNS settings via Network Manager. Changes usually persist across reboots and network changes.

nmcli: For systems using NetworkManager, nmcli can modify DNS settings. \
To set DNS servers on a specific connection: \
`nmcli con mod <connection_name> ipv4.dns "<DNS_servers>"` \
`nmcli con mod <connection_name> ipv6.dns "<DNS_servers>"`

To reload the connection and apply changes:\
&#x20;`nmcli con up <connection_name>`

### <mark style="color:purple;">dhclient</mark>

dhclient: If your system uses DHCP to obtain network settings, including DNS, you might need to modify the DHCP client configuration to change DNS behavior. \


The configuration file might vary, but commonly /etc/dhcp/dhclient.conf is used. \


You can specify `prepend domain-name-servers <DNS_server_IP>`; to add custom DNS servers. \


Example command to edit dhclient.conf: \
`sudo vi /etc/dhcp/dhclient.conf`

### <mark style="color:purple;">Distribution-Specific Tools</mark>

Debian/Ubuntu: Use `resolvconf` to manage resolv.conf dynamically.

Red Hat/CentOS: Use `systemd-resolved` to manage DNS configuration. systemd-resolve or resolvectl: On systems using systemd-resolved, this tool manages DNS settings. \


To set global DNS servers: \` sudo systemd-resolve --set-dns=\<DNS\_server\_IP> --interface=\<interface\_name>

To set DNS domains for searches: \` sudo systemd-resolve --set-domain= --interface=\<interface\_name>

## <mark style="color:red;">Routing Tables</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="592">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>ip route add &#x3C;network>/&#x3C;prefix> via &#x3C;gateway></code></td><td>Add a route</td></tr><tr><td><code>route add -net &#x3C;network> netmask &#x3C;netmask> gw &#x3C;gateway></code></td><td>Add a route</td></tr><tr><td><code>ip route del &#x3C;network>/&#x3C;prefix></code></td><td>Delete a route</td></tr><tr><td><code>route del -net &#x3C;network> netmask &#x3C;netmask></code></td><td>Delete a route</td></tr><tr><td><code>ip route add default via &#x3C;gateway></code></td><td>Change the default gateway</td></tr><tr><td><code>route add default gw &#x3C;gateway></code></td><td>Change the default gateway</td></tr><tr><td><code>ip route flush all</code></td><td>Flush all routes</td></tr></tbody></table>

### <mark style="color:purple;">Config Files (persistent changes)</mark>

Edit /etc/network/interfaces (Debian/Ubuntu): Add `post-up` or `pre-up` commands to execute routing commands after interface activation.&#x20;

Edit /etc/sysconfig/network-scripts/route-\<interface> (Red Hat/CentOS): Add routing rules directly to configuration files.

## <mark style="color:red;">Sockets</mark>

Adjusts the range of ports available for user-space applications:\
`sysctl -w net.ipv4.ip_local_port_range="1024 65535"`

Enables reuse of sockets in TIME-WAIT state for new connections, affecting how sockets are managed: \
`sysctl -w net.ipv4.tcp_tw_reuse=1`

Uses Uncomplicated Firewall (ufw) to allow or deny access to specific ports on Ubuntu and other systems: \
`ufw allow|deny [port]`

Allows incoming TCP connections on a specific port. Modify rules to control access to sockets: \
`iptables -A INPUT -p tcp --dport [port] -j ACCEPT`

The easiest way to open and close ports is to kill/disable the process/service using it. \
Otherwise, you can make firewall/iptable rules to block/allow/etc.
