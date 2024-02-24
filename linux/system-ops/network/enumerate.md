# Enumerate

## <mark style="color:red;">NICs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="443">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>ifconfig -a</code></td><td>Prints network information/configuration.</td></tr><tr><td><code>ifconfig eth0</code></td><td>Specific interface</td></tr><tr><td><code>ip addr show</code></td><td>Show NIC Info</td></tr><tr><td><code>ip addr show eth0</code></td><td>Specific interface</td></tr><tr><td><code>netstat -I</code></td><td>Shows interface stats.</td></tr><tr><td><code>netstat -ie</code></td><td>Shows interface stats, including MAC addresses.</td></tr><tr><td><code>ip link show</code></td><td>Shows the state of all network interfaces.</td></tr><tr><td><code>ls /sys/class/net/</code></td><td>Lists all network interfaces recognized by the kernel</td></tr><tr><td><code>lspci | grep -i network</code></td><td>Lists all PCI network interfaces by searching for "network"</td></tr><tr><td><code>nmcli device status</code></td><td>Lists network devices and their status using the NetworkManager command-line tool</td></tr><tr><td><code>nmtui</code></td><td>Provides a text user interface to NetworkManager</td></tr><tr><td><code>ethtool &#x3C;interface></code></td><td>Shows detailed info about a specific Eth interface</td></tr><tr><td><code>lshw -class network</code></td><td>Detailed info on all network interfaces. Requires <code>lshw</code> to be installed.</td></tr><tr><td><code>cat /sys/class/net/&#x3C;interface>/address</code></td><td>Directly reads the MAC address from the system's file</td></tr></tbody></table>

### <mark style="color:purple;">Wireless</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="438">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>iwconfig</code></td><td>Displays wireless network configuration.</td></tr><tr><td><code>iw dev</code></td><td>Lists all wireless interfaces along with their details, including MAC addresses. Requires <code>iw</code> for wireless device operations.</td></tr></tbody></table>

## <mark style="color:red;">ARP</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="435">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>arp</code></td><td>Displays the current ARP table/cache for the system.</td></tr><tr><td><code>arp -a</code></td><td>More readable format.</td></tr><tr><td><code>arp -an</code></td><td>Print the ARP cache.</td></tr><tr><td><code>ip neigh</code></td><td>Shows the ARP table. On newer systems. Part of 'iproute2'.</td></tr><tr><td><code>ip neigh show</code></td><td>List the entries.</td></tr><tr><td><code>ip -s -s neigh</code></td><td>Shows statistics about the ARP cache (size, entries, hits and misses).</td></tr><tr><td><code>arp-scan</code></td><td>Sends ARP packets to local network to discover IP and MAC addresses. Needs install.</td></tr><tr><td><code>cat /proc/net/arp</code></td><td>Displays the ARP table by reading the kernel's ARP table file.</td></tr></tbody></table>

## <mark style="color:red;">DNS</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="435">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>dig &#x3C;domain></code></td><td>Queries DNS servers for info about domain names.</td></tr><tr><td><code>drill &#x3C;domain></code></td><td>Similar to <code>dig</code>, supports DNSSEC.</td></tr><tr><td><code>host &#x3C;domain></code></td><td>Shows IP address and basic DNS information.</td></tr><tr><td><code>nslookup &#x3C;hostname/IP></code></td><td>Queries Internet domain name servers for DNS lookup.</td></tr><tr><td><code>whois &#x3C;domain></code></td><td>Retrieves domain registration info.</td></tr><tr><td><code>nmcli device show</code></td><td>For systems using NetworkManager, includes DNS settings for network interfaces.</td></tr><tr><td><code>scutil --dns</code></td><td>(macOS specific) Displays the DNS config.</td></tr><tr><td><code>cat /etc/resolv.conf</code></td><td>Display DNS configuration.</td></tr><tr><td><code>cat /etc/hosts</code></td><td>Display hosts file.</td></tr></tbody></table>

Shows detailed DNS config and stats for systems using `systemd-resolved` for managing network name resolution. \
It provides information about global and per-link DNS settings: `systemd-resolve --status`

Checks for DNS servers configured in network interface files (if applicable):\
`grep nameserver /etc/network/interfaces` \
`grep nameserver /etc/sysconfig/network`

## <mark style="color:red;">Routing Tables</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="431">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>netstat -rn</code></td><td>Prints the kernel routing tables.</td></tr><tr><td><code>route -n</code></td><td>Displays the routing table in a numerical format, making it easier to parse.</td></tr><tr><td><code>ip route show</code></td><td>Lists the kernel routing tables. (Newer Linux command)</td></tr><tr><td><code>ip route list</code></td><td>Similar to <code>ip route show</code>.</td></tr><tr><td><code>ip route</code></td><td>Displays the routing table.</td></tr><tr><td><code>ss -r</code></td><td>Shows socket statistics with routing information. Not a direct way to list the routing table.</td></tr><tr><td><code>cat /proc/net/route</code></td><td>Displays the routing table from the system's proc filesystem.</td></tr><tr><td><code>ip route get &#x3C;destination></code></td><td>Traces the route to a specific destination.</td></tr><tr><td><code>traceroute &#x3C;hostname/IP></code></td><td>Traces the path packets take to reach a host, helping to identify network bottlenecks.</td></tr><tr><td><code>mtr &#x3C;hostname/IP></code></td><td>Combines <code>ping</code> and <code>traceroute</code> functionalities to provide continuous network diagnostics.</td></tr></tbody></table>

## <mark style="color:red;">Sockets</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="431">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>ss -auntp</code></td><td>TCP connections and listeners, UDP listeners, and Processes.</td></tr><tr><td><code>netstat -auntp</code></td><td>TCP connections and listeners, UDP listeners, and PIDs.</td></tr></tbody></table>

### <mark style="color:purple;">Netstat Options</mark>

<table data-header-hidden data-full-width="false"><thead><tr><th width="240">Option</th><th>Description</th></tr></thead><tbody><tr><td><code>-a</code></td><td>Show both listening and non-listening sockets.</td></tr><tr><td><code>-t</code></td><td>Show TCP connections.</td></tr><tr><td><code>-u</code></td><td>Show UDP connections.</td></tr><tr><td><code>-n</code></td><td>Show numerical addresses instead of resolving hostnames.</td></tr><tr><td><code>-l</code></td><td>Show only listening sockets.</td></tr><tr><td><code>-p</code></td><td>Show the PID and name of the program to which each socket belongs.</td></tr><tr><td><code>-r</code></td><td>Display the routing table.</td></tr><tr><td><code>-i</code></td><td>Display a table of all network interfaces.</td></tr><tr><td><code>-s</code></td><td>Show statistics for all protocols.</td></tr><tr><td><code>-c</code></td><td>Continuously list the information.</td></tr><tr><td><code>-W</code></td><td>Avoid truncating IP addresses (useful for IPv6).</td></tr><tr><td><code>-e</code></td><td>Display extended information; more detailed.</td></tr><tr><td><code>-o</code></td><td>Show timer information (similar to <code>ss -o</code>).</td></tr><tr><td><code>-g</code></td><td>Display multicast group memberships.</td></tr><tr><td><code>-C</code></td><td>Show the routing cache.</td></tr><tr><td><code>-A &#x3C;family></code></td><td>Specify the address family (e.g., <code>inet</code>, <code>inet6</code>, <code>unix</code>).</td></tr><tr><td><code>-F</code></td><td>Display the Forwarding Information Base (FIB).</td></tr><tr><td><code>-M</code></td><td>Display masqueraded connections.</td></tr><tr><td><code>-x</code></td><td>Show UNIX domain sockets.</td></tr><tr><td><code>-Z</code></td><td>Show the SELinux security context for sockets.</td></tr><tr><td><code>--numeric-hosts</code></td><td>Show hosts numerically (avoid DNS lookup).</td></tr><tr><td><code>--numeric-ports</code></td><td>Show ports numerically.</td></tr><tr><td><code>--numeric-users</code></td><td>Show users numerically (avoid user name lookup).</td></tr><tr><td><code>--protocol=&#x3C;family></code></td><td>Show information for a specific protocol family.</td></tr><tr><td><code>--tcp</code></td><td>Shortcut for <code>-A inet -t</code>.</td></tr><tr><td><code>--udp</code></td><td>Shortcut for <code>-A inet -u</code>.</td></tr><tr><td><code>--unix</code></td><td>Shortcut for <code>-A unix -x</code>.</td></tr><tr><td><code>--inet</code></td><td>Shortcut for specifying IPv4 protocols only.</td></tr><tr><td><code>--inet6</code></td><td>Shortcut for specifying IPv6 protocols only.</td></tr></tbody></table>

### <mark style="color:purple;">SS Options</mark>

<table data-header-hidden><thead><tr><th width="241">Option</th><th>Description</th></tr></thead><tbody><tr><td><code>-h</code></td><td>Display help message.</td></tr><tr><td><code>-V</code></td><td>Show version info.</td></tr><tr><td><code>-n</code></td><td>Do not resolve service names (show numerical addresses and ports).</td></tr><tr><td><code>-r</code></td><td>Resolve hostnames (inverse of -n).</td></tr><tr><td><code>-a</code></td><td>Both listening and non-listening sockets.</td></tr><tr><td><code>-l</code></td><td>Listening sockets only.</td></tr><tr><td><code>-o</code></td><td>Show timer info.</td></tr><tr><td><code>-m</code></td><td>Show memory usage for each socket.</td></tr><tr><td><code>-p</code></td><td>Show process using the socket.</td></tr><tr><td><code>-i</code></td><td>Show internal TCP info.</td></tr><tr><td><code>-s</code></td><td>Show socket usage statistics.</td></tr><tr><td><code>-4</code></td><td>IPv4 sockets only.</td></tr><tr><td><code>-6</code></td><td>IPv6 sockets only.</td></tr><tr><td><code>-0</code></td><td>Packet sockets only.</td></tr><tr><td><code>-t</code></td><td>TCP sockets only.</td></tr><tr><td><code>-u</code></td><td>UDP sockets only.</td></tr><tr><td><code>-d</code></td><td>DCCP sockets only.</td></tr><tr><td><code>-w</code></td><td>RAW sockets only.</td></tr><tr><td><code>-x</code></td><td>Unix domain sockets only.</td></tr><tr><td><code>-f</code></td><td>Specify address family (use with <code>inet</code>, <code>unix</code>, <code>link</code>, <code>netlink</code>, <code>inet6</code>, etc.).</td></tr><tr><td><code>-A</code></td><td>Filter sockets by states (e.g., <code>all</code>, <code>connected</code>, <code>synchronized</code>, <code>bucket</code>, <code>big</code>).</td></tr><tr><td><code>-e</code></td><td>Show detailed socket info.</td></tr><tr><td><code>-E</code></td><td>Export socket info to a file.</td></tr><tr><td><code>-Z</code></td><td>Show socket security info.</td></tr><tr><td><code>-K</code></td><td>Show TCP congestion algorithm.</td></tr><tr><td><code>-c</code></td><td>Show continuous listing.</td></tr><tr><td><code>-S</code></td><td>Show socket details in summary format.</td></tr><tr><td><code>-b</code></td><td>Show BPF filter socket info.</td></tr><tr><td><code>-N &#x3C;netns></code></td><td>Switch to the specified network namespace (requires either PID or name of the netns).</td></tr><tr><td><code>-H</code></td><td>Do not print header.</td></tr><tr><td><code>state &#x3C;filter></code></td><td>Filter sockets by state (e.g., <code>established</code>, <code>time-wait</code>).</td></tr></tbody></table>

## <mark style="color:red;">Connectivity</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="353">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>ping &#x3C;hostname/IP></code></td><td>Tests connectivity to a host and measures round-trip time.</td></tr><tr><td><code>traceroute &#x3C;hostname/IP></code></td><td>Traces the path packets take to reach a host, helping identify network bottlenecks.</td></tr><tr><td><code>mtr &#x3C;hostname/IP></code></td><td>Combines <code>ping</code> and <code>traceroute</code> functionalities.</td></tr><tr><td><code>nc &#x3C;hostname/IP> &#x3C;port></code></td><td>Tests TCP connectivity to a specified port on a host.</td></tr><tr><td><code>telnet &#x3C;hostname/IP> &#x3C;port></code></td><td>Attempts to establish a TCP connection to a specified port on a host.</td></tr><tr><td><code>curl &#x3C;URL></code></td><td>Retrieves content from a web server, useful for testing HTTP connectivity.</td></tr><tr><td><code>host &#x3C;hostname></code></td><td>Simple utility for DNS lookups.</td></tr><tr><td><code>iperf / iperf3</code></td><td>Measures the maximum network bandwidth between a client and a server.</td></tr></tbody></table>

## <mark style="color:red;">Processes Using Network</mark>

<table data-header-hidden data-full-width="false"><thead><tr><th width="284">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>lsof -i</code></td><td>Lists open files belonging to active network connections.</td></tr><tr><td><code>sudo lsof -i tcp:&#x3C;port></code></td><td>Lists processes using a specific TCP port.</td></tr><tr><td><code>sudo lsof -i udp:&#x3C;port></code></td><td>Lists processes using a specific UDP port.</td></tr><tr><td><code>netstat -tupln</code></td><td>Shows the PID and program name that are listening.</td></tr><tr><td><code>ss -tupln</code></td><td>Shows the PID and program name that are listening.</td></tr><tr><td><code>nethogs</code></td><td>Displays real-time network usage per process.</td></tr></tbody></table>

### <mark style="color:purple;">Find Processes Using a Specific Port</mark>

Use with caution as it sends signals to processes and could affect their behavior:

<table data-header-hidden><thead><tr><th width="280">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>fuser &#x3C;port></code></td><td>Provides PID</td></tr><tr><td><code>fuser -nv tcp &#x3C;port></code></td><td>Identifies processes using a specific TCP port</td></tr><tr><td><code>fuser -nv udp &#x3C;port></code></td><td>Identifies processes using a specific UDP port.</td></tr></tbody></table>

### <mark style="color:purple;">Find Processes that have Port Information</mark>

```bash
pfiles \ `ptree | awk '{print $1}'\`| egrep '^[0-9]|port:'
```

Captures TCP packets with SYN or ACK flags, indicating connection attempts. Requires root privileges:&#x20;

```bash
tcpdump -i <interface> -n 'tcp[tcpflags] & (tcp-syn|tcp-ack) != 0'
```

Sets up a rule in iptables to log network connections initiated by processes owned by a specific user. This requires analyzing the log to see the connections:

```bash
iptables -A OUTPUT -m owner --uid-owner <user> -j LOG
```

## <mark style="color:red;">Solaris</mark>

`netstat -anP tcp`\
`netstat -anP udp`\
`pfiles /proc/`\
``pfiles `ptree | awk '{print $1}'`| egrep '^[0-9]|port:' >> /tmp/ports rpcinfo -p``
