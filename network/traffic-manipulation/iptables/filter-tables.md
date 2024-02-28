# Filter Tables

Default table and is primarily used for packet filtering.

## <mark style="color:red;">Chains</mark>

<table data-header-hidden><thead><tr><th width="172">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>INPUT</code></mark></td><td>Examined when packets ARRIVE at the system.</td></tr><tr><td><mark style="color:yellow;"><code>OUTPUT</code></mark></td><td>Applied as packets are SENT FROM the system.</td></tr><tr><td><mark style="color:yellow;"><code>FORWARD</code></mark></td><td>Checked as packets are ROUTED THROUGH the system.</td></tr></tbody></table>

## <mark style="color:red;">Actions</mark>

<mark style="color:yellow;">`ACCEPT`</mark>&#x20;

<mark style="color:yellow;">`REJECT`</mark>&#x20;

<mark style="color:yellow;">`DROP`</mark>

## <mark style="color:red;">Examples by Chain</mark>

### <mark style="color:purple;">INPUT/OUTPUT</mark>

Allow loopback traffic

```bash
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A OUTPUT -o lo -j ACCEPT
```

Allow established and related connections INCOMING and OUTGOING

```bash
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
sudo iptables -A OUTPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

Allow incoming SSH traffic from a specific IP range

```bash
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j ACCEPT
```

Allow incoming ICMP (ping) traffic

```bash
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
```

Allow incoming FTP traffic

{% code overflow="wrap" %}
```bash
sudo iptables -A INPUT -p tcp --dport 21 -j ACCEPT
sudo iptables -A INPUT -p tcp --sport 20 -m state --state RELATED,ESTABLISHED -j ACCEPT
```
{% endcode %}

Allow incoming and outgoing DNS traffic

```bash
sudo iptables -A INPUT -p udp --dport 53 -j ACCEPT
sudo iptables -A OUTPUT -p udp --dport 53 -j ACCEPT
```

Allow incoming and outgoing NTP traffic

```bash
sudo iptables -A INPUT -p udp --dport 123 -j ACCEPT
sudo iptables -A OUTPUT -p udp --dport 123 -j ACCEPT
```

Allow outgoing SMTP (email) traffic

```bash
sudo iptables -A OUTPUT -p tcp --dport 25 -j ACCEPT
```

Allow outgoing IMAP and IMAPS (email) traffic

```bash
sudo iptables -A OUTPUT -p tcp --dport 143 -j ACCEPT
sudo iptables -A OUTPUT -p tcp --dport 993 -j ACCEPT
```

Allow outgoing HTTP and HTTPS traffic

```bash
sudo iptables -A OUTPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A OUTPUT -p tcp --dport 443 -j ACCEPT
```

Allow outgoing FTP traffic

{% code overflow="wrap" %}
```bash
sudo iptables -A OUTPUT -p tcp --dport 21 -j ACCEPT
sudo iptables -A OUTPUT -p tcp --sport 20 -m state --state RELATED,ESTABLISHED -j ACCEPT
```
{% endcode %}

Allow INCOMING traffic by PORT:

{% code overflow="wrap" %}
```bash
sudo iptables -t filter -A INPUT -p TCP -m multiport --ports 22,23,3389,6001:6030 -j ACCEPT
```
{% endcode %}

Allow OUTGOING traffic by PORT:

{% code overflow="wrap" %}
```bash
sudo iptables -t filter -A OUTPUT -p TCP -m multiport --ports 22,23,3389,6001:6030 -j ACCEPT
```
{% endcode %}

Limit incoming SSH connections per minute and block brute-force attacks

{% code overflow="wrap" %}
```bash
sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -m recent --set

sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -m recent --update --seconds 60 --hitcount 4 -j DROP

sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
{% endcode %}

Log and drop invalid packets

{% code overflow="wrap" %}
```bash
sudo iptables -A INPUT -m conntrack --ctstate INVALID -j LOG --log-prefix "INVALID_PACKET: " --log-ip-options --log-tcp-options

sudo iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
```
{% endcode %}

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t filter -A INPUT -i lo -j ACCEPT</code></mark></td><td>Append rule to accept all INCOMING traffic on the loopback interface</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t filter -A INPUT -p tcp --dport 22 -j ACCEPT</code></mark></td><td>Append a rule to accept SSH traffic (port 22) in the INPUT chain.</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t filter -A INPUT -p icmp -j DROP</code></mark></td><td>Append a rule to drop all ICMP traffic in the INPUT chain.</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t filter -I INPUT 1 -s 192.168.1.1 -j DROP</code></mark></td><td>Insert a rule at the top of the INPUT chain to drop traffic from IP 192.168.1.1.</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t filter -R INPUT 1 -p tcp --dport 80 -j ACCEPT</code></mark></td><td>Replace the first rule in the INPUT chain with a new one to accept HTTP traffic (port 80).</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t filter -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT</code></mark></td><td>Append a rule to accept all established and related connections in the INPUT chain.</td></tr></tbody></table>

### <mark style="color:purple;">FORWARD</mark>

Allow all forwarded traffic (not secure, but useful for open forwarding)

```bash
iptables -A FORWARD -j ACCEPT
```

Drop all forwarded traffic (default policy for a secure stance)

```bash
iptables -A FORWARD -j DROP
```

Allow forwarded traffic from a specific source IP

```bash
iptables -A FORWARD -s 192.168.1.100 -j ACCEPT
```

Allow forwarded traffic to a specific destination IP

```bash
iptables -A FORWARD -d 192.168.2.100 -j ACCEPT
```

Allow forwarded traffic from a specific subnet to another subnet

```bash
iptables -A FORWARD -s 192.168.1.0/24 -d 192.168.2.0/24 -j ACCEPT
```

Drop forwarded traffic from a specific subnet to any destination

```bash
iptables -A FORWARD -s 10.10.0.0/16 -j DROP
```

Allow forwarded traffic on a specific port (e.g., HTTP)

```bash
iptables -A FORWARD -p tcp --dport 80 -j ACCEPT
```

Log and then drop forwarded packets from a specific IP

```bash
iptables -A FORWARD -s 10.10.10.10 -j LOG --log-prefix "Dropped by iptables: "
iptables -A FORWARD -s 10.10.10.10 -j DROP
```

Limiting forwarded traffic rate from a specific source (e.g., 5 packets per second)

```bash
iptables -A FORWARD -s 192.168.1.100 -m limit --limit 5/sec -j ACCEPT
iptables -A FORWARD -s 192.168.1.100 -j DROP
```

Reject forwarded traffic to a specific port with a custom TCP reset

```bash
iptables -A FORWARD -p tcp --dport 22 -j REJECT --reject-with tcp-reset
```

Allow forwarded traffic but ensure stateful inspection (connection tracking)

```bash
iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -m state --state NEW -i eth1 -o eth0 -j ACCEPT
```

## <mark style="color:red;">Examples by Match Statements</mark>

### <mark style="color:purple;">Multiport</mark>

Block Incoming Traffic on Multiple Ports:

```bash
iptables -A INPUT -p tcp -m multiport --dports 80,443,8080 -j DROP
```

Allow Outgoing Traffic on Multiple Ports:

```bash
iptables -A OUTPUT -p tcp -m multiport --sports 21,22,25 -j ACCEPT
```

Restricting Access to Specific IP Addresses on Multiple Ports:

```bash
iptables -A INPUT -p tcp -s 192.168.1.100 -m multiport --dports 80,443 -j ACCEPT
```

Block Outgoing Traffic to Multiple Ports Except for a Specific IP Address:

{% code overflow="wrap" %}
```bash
iptables -A OUTPUT -p tcp ! -d 192.168.1.50 -m multiport --dports 25,465,587 -j REJECT
```
{% endcode %}

Logging Packets That Match Multiport Rules:

{% code overflow="wrap" %}
```bash
iptables -A INPUT -p tcp -m multiport --dports 80,443,8080 -j LOG --log-prefix "Dropped Packet: "

iptables -A INPUT -p tcp -m multiport --dports 80,443,8080 -j DROP
```
{% endcode %}

### <mark style="color:purple;">State/Conntrack</mark>

Allow Established and Related Incoming Connections

Allows incoming packets that are part of an established connection or are related to an established connection.

Useful for ensuring that once a connection is initiated, its packets can continue to flow:

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

Drop Invalid Packets:

```bash
iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
```

Allow New, Established, and Related Outgoing Connections:

```bash
iptables -A OUTPUT -m conntrack --ctstate NEW,ESTABLISHED,RELATED -j ACCEPT
```

Allow New SSH Connections From a Specific IP Address:

{% code overflow="wrap" %}
```bash
iptables -A INPUT -p tcp --dport 22 -s 192.168.1.100 -m conntrack --ctstate NEW -j ACCEPT
```
{% endcode %}

Block New Incoming Connections on a Specific Port

Allows established and related connections.

It's a common security measure to prevent unauthorized access while allowing ongoing SSH sessions:

```bash
iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW -j DROP
```

Logging New Incoming Connections:

```bash
iptables -A INPUT -m conntrack --ctstate NEW -j LOG --log-prefix "New Connection: "
```

Limiting New Connections Per Second From a Single Source:

<pre class="language-bash" data-overflow="wrap"><code class="lang-bash">iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -m limit --limit 1/s --limit-burst 5 -j ACCEPT
<strong>
</strong><strong>iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -j DROP
</strong></code></pre>

### <mark style="color:purple;">iprange</mark>

Allow Traffic to a Specific Port from a Range of IP Addresses:

{% code overflow="wrap" %}
```bash
iptables -A INPUT -p tcp --dport 80 -m iprange --src-range 10.0.0.1-10.0.0.255 -j ACCEPT
```
{% endcode %}

Block Outgoing Traffic to a Specific IP Range:

```bash
iptables -A OUTPUT -m iprange --dst-range 203.0.113.0-203.0.113.255 -j DROP
```

Limiting Forward Traffic from a Specific IP Range:

```bash
iptables -A FORWARD -m iprange --src-range 172.16.0.0-172.16.255.255 -j ACCEPT
```

Rejecting Incoming Connections to a Range of IP Addresses:

```bash
iptables -A INPUT -m iprange --dst-range 10.10.10.1-10.10.10.100 -j REJECT
```

### <mark style="color:purple;">icmp</mark>

Block All Incoming ICMP Echo Requests (Ping Requests)

````bash
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```bash

Allow ICMP Echo Replies
```bash
iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
````

Limit Incoming ICMP Echo Requests

{% code overflow="wrap" %}
```bash
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s --limit-burst 4 -j ACCEPT

iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```
{% endcode %}

Allow ICMP Destination Unreachable

```bash
iptables -A INPUT -p icmp --icmp-type destination-unreachable -j ACCEPT
```

Block ICMP Timestamp Requests

```bash
iptables -A INPUT -p icmp --icmp-type timestamp-request -j DROP
```

Allow ICMP Fragmentation Needed for Path MTU Discovery

```bash
iptables -A INPUT -p icmp --icmp-type fragmentation-needed -j ACCEPT
```
