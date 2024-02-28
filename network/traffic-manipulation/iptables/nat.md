# NAT

Used to modify the source or destination address of packets as they pass through.

## <mark style="color:red;">Chains</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="191">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>PREROUTING</code></mark></td><td>Engaged for incoming packets before any routing decision is made, suitable for DNAT.</td></tr><tr><td><mark style="color:yellow;"><code>POSTROUTING</code></mark></td><td>Activated for outgoing packets after all routing decisions have been made, ideal for SNAT and masquerading.</td></tr><tr><td><mark style="color:yellow;"><code>OUTPUT</code></mark></td><td>Applied to locally generated packets before they are sent out, allowing for DNAT on outgoing traffic.</td></tr></tbody></table>

## <mark style="color:red;">Actions</mark>

### <mark style="color:purple;">DNAT</mark>

Modifies the destination address (and optionally the port) of incoming packets.

Primarily used with PREROUTING and OUPUT to redirect to IP or Post

Uses: Portforwarding, load balancing, or directing traffic to internal servers that are hidden behind a firewall or NAT device.

### <mark style="color:purple;">SNAT</mark>

Changes the source address (and optionally the port) of outgoing packets.

Used in POSTROUTING to alter the packet's source address for outgoing packets.

Crucial for scenarios where multiple private IP addresses need to be masqueraded as a single public IP address.

### <mark style="color:purple;">MASQUERADE</mark>

Special form of SNAT for dynamically assigned IPs, such as those found with DHCP.

Automatically uses the current IP of the outgoing network interface, eliminating the need to specify a specific IP address.

Useful for connections with dynamic external IPs.

### <mark style="color:purple;">REDIRECT</mark>

Alters the destination port or address to the local machine.

Typically used in the PREROUTING and OUTPUT for transparent proxying, where the packet's destination is modified to redirect the traffic to a local service without changing the packet's destination IP.

### <mark style="color:purple;">RETURN</mark>

Stops processing in the current chain and returns to the previous chain from which the packet came.

Not specific to NAT operations.

Can be used within user-defined chains in the "nat" table to halt processing and allow the packet to be evaluated against the subsequent rules in the original chain.

## <mark style="color:red;">Examples by Chain</mark>

### <mark style="color:purple;">PREROUTING</mark>

#### <mark style="color:green;">Port forwarding to a Local Server:</mark>

Redirects traffic destined for a specific port on the public interface to a different port on a private server behind the firewall.

{% code overflow="wrap" %}
```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.10:8080
```
{% endcode %}

#### <mark style="color:green;">Masquerading:</mark>

Translates the private addresses of internal machines behind the firewall to the public IP of the firewall for outgoing traffic.

```bash
iptables -t nat -A PREROUTING -o eth0 -j MASQUERADE
```

#### <mark style="color:green;">Load balancing:</mark>

Distributes traffic across multiple internal servers by redirecting requests to different ports based on a specific criteria.

{% code overflow="wrap" %}
```bash
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -m iprange --src-range 192.168.1.0/24 -j DNAT --to-destination 192.168.1.10:80

iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -m iprange --src-range 192.168.1.128/24 -j DNAT --to-destination 192.168.1.20:80
```
{% endcode %}

Redirecting All Incoming Traffic to a Specific Port

```bash
iptables -t nat -A PREROUTING -p tcp --dport 8080 -j REDIRECT --to-port 80
```

#### <mark style="color:green;">Transparent Proxy:</mark>

If you're running a proxy server on your network (e.g., Squid running on port 3128), you can redirect all outgoing HTTP traffic to go through the proxy without configuring each client.

This example assumes the proxy server is on the same machine where iptables is being configured.

```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 3128
```

### <mark style="color:purple;">POSTROUTING</mark>

Masquerading Outgoing Traffic:

```bash
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

Masquerading Based on Source IP:

```bash
iptables -t nat -A POSTROUTING -s 10.10.1.0/24 -o eth0 -j MASQUERADE
```

Masquerading Based on Destination:

```bash
iptables -t nat -A POSTROUTING -o eth0 -d 192.168.2.0/24 -j MASQUERADE
```

SNAT Translates the private IPs of internal machines behind the firewall to a specific public IP when they initiate outgoing connections

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.1.0/24 -j SNAT --to-source 10.0.0.1
```
{% endcode %}

All internal IPs:

```bash
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 10.0.0.1
```

<mark style="color:yellow;">`--to-source 10.0.0.1`</mark> Specifies the new source IP address for outgoing packets.

SNAT with Multiple IPs:

```bash
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 203.0.113.5-203.0.113.10
```

Port masking:

```bash
iptables -t nat -A POSTROUTING -o eth0 -p tcp --dport 80 -j MASQUERADE
```

#### <mark style="color:green;">Network Address Translation (NAT) Hairpinning:</mark>

Allows internal servers to access resources hosted on other internal servers while using their private IP addresses, even though they share the same public IP.

```bash
iptables -t nat -A POSTROUTING -o eth0 -d 192.168.1.0/24 -j SNAT --to-source 10.0.0.1
```

Outbound traffic filtering:

```bash
iptables -t nat -A POSTROUTING -o eth0 -d 192.168.2.0/24 -p tcp --dport 25 -j DROP
```

### <mark style="color:purple;">OUTPUT</mark>

While the OUTPUT chain in the iptables NAT table exists, it is generally not recommended to use it for NAT operations.

Limited Functionality:

Compared to PREROUTING and POSTROUTING, OUTPUT has limited NAT capabilities.

It can only perform Destination NAT (DNAT), modifying the destination address of outgoing packets.

It cannot manipulate source addresses or perform other NAT operations like masquerading.

Redundancy:

The functionalities achievable with OUTPUT chain DNAT can often be achieved more efficiently and transparently through other chains:

For local server DNAT: Use PREROUTING chain DNAT, as it directly affects incoming packets heading to your server.

For masquerading: Use POSTROUTING chain SNAT, which automatically translates private addresses for all outgoing traffic.

Potential Risks: Modifying outbound packets within the OUTPUT chain can sometimes create unexpected behavior or interfere with applications.

However, for educational purposes, here's an example of using OUTPUT chain DNAT:

{% code overflow="wrap" %}
```bash
iptables -t nat -A OUTPUT -p tcp --dport 80 -d google.com -j DNAT --to-destination 192.168.1.10:80
```
{% endcode %}

## <mark style="color:red;">Examples by Action</mark>

### <mark style="color:purple;">DNAT</mark>

#### <mark style="color:green;">PREROUTING:</mark>

Port forwarding: Redirects traffic destined for a public port to a different port on a private server:

{% code overflow="wrap" %}
```bash
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to-destination 192.168.1.10:8080
```
{% endcode %}

Port forwarding: Redirecting all incoming HTTP traffic to a different server.

{% code overflow="wrap" %}
```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.100:8080
```
{% endcode %}

Load balancing: This rule distributes traffic across multiple internal servers based on source IP range:

{% code overflow="wrap" %}
```bash
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -m iprange --src-range 192.168.1.0/24 -j DNAT --to-destination 192.168.1.10:80

iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -m iprange --src-range 192.168.1.128/24 -j DNAT --to-destination 192.168.1.20:80
```
{% endcode %}

Transparent proxy: This rule redirects all traffic to a transparent proxy server:

```bash
iptables -t nat -A PREROUTING -i eth0 -j DNAT --to-destination 192.168.1.25:8080
```

Forwarding Traffic to a VPN or Proxy Server:

```bash
iptables -t nat -A PREROUTING -d 203.0.113.5 -j DNAT --to-destination 10.8.0.1
```

#### <mark style="color:green;">POSTROUTING:</mark>

Hairpinning: This rule allows internal servers to access each other using private IPs:

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -o eth0 -d 192.168.1.0/24 -j DNAT --to-source 10.0.0.1
```
{% endcode %}

Masquerading: This rule translates private addresses to a public IP for outgoing traffic:

```bash
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.1.0/24 -j SNAT --to-s
```

### <mark style="color:purple;">SNAT</mark>

#### <mark style="color:green;">POSTROUTING:</mark>

Masquerading all outgoing traffic: This translates all private IPs from your internal network to a single public IP when leaving the network.

```bash
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 10.0.0.1
```

SNAT specific internal subnet: Translate addresses from a specific subnet to a different public IP.

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.2.0/24 -j SNAT --to-source 10.0.0.2
```
{% endcode %}

Port-specific SNAT: Translate the source IP only for specific ports (e.g., for outbound gaming traffic).

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -o eth0 -p tcp --dport 27015 -j SNAT --to-source 10.0.0.3
```
{% endcode %}

SNAT with Multiple Public IP Addresses: If your gateway has multiple public IP addresses, you can use SNAT to distribute outgoing traffic across these IPs.

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o eth0 -j SNAT --to-source 203.0.113.3-203.0.113.4
```
{% endcode %}

SNAT for Specific Services: Change the source IP for specified service by port.

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -p tcp --dport 80 -o eth0 -j SNAT --to-source 203.0.113.5
```
{% endcode %}

Change source IP of outgoing packets from the 10.10.10.0/24 network to 192.168.1.1:

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -s 10.10.10.0/24 -o eth0 -j SNAT --to-source 192.168.1.1
```
{% endcode %}

Translates the private IPs of internal machines behind the firewall to a specific public IP when they initiate outgoing connections

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.1.0/24 -j SNAT --to-source 10.0.0.1
```
{% endcode %}

All internal IPs:

```bash
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 203.0.113.5
```

<mark style="color:yellow;">`--to-source 203.0.113.5`</mark> Specifies the new source IP for outgoing packets.

SNAT with Multiple IPs:

```bash
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 203.0.113.5-203.0.113.10
```

Network Address Translation (NAT) Hairpinning:

Allows internal servers to access resources hosted on other internal servers while using their private IP addresses, even though they share the same public IP.

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -o eth0 -d 192.168.1.0/24 -j SNAT --to-source 10.0.0.1
```
{% endcode %}

#### <mark style="color:green;">PREROUTING:</mark>

SNAT incoming traffic for specific destination: Change the source IP of incoming traffic destined for a specific server.

```bash
iptables -t nat -A PREROUTING -i eth0 -d 192.168.1.20 -j SNAT --to-source 10.0.0.4
```

### <mark style="color:purple;">MASQUERADE</mark>

Masquerading a private network's outgoing traffic to match the public IP of the router, especially when the router's IP is assigned dynamically.

#### <mark style="color:green;">POSTROUTING:</mark>

Masquerading all outgoing traffic: This is the most common scenario, translating all private IP addresses from your internal network to the public IP of the firewall.

```bash
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

Masquerading specific internal subnet: You can restrict masquerading to a specific subnet within your internal network.

```bash
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.2.0/24 -j MASQUERADE
```

Masquerading Based on Source IP:

```bash
iptables -t nat -A POSTROUTING -s 10.10.1.0/24 -o eth0 -j MASQUERADE
```

Masquerading Based on Destination:

```bash
iptables -t nat -A POSTROUTING -o eth0 -d 192.168.2.0/24 -j MASQUERADE
```

Port masking:

```bash
iptables -t nat -A POSTROUTING -o eth0 -p tcp --dport 80 -j MASQUERADE
```

#### <mark style="color:green;">PREROUTING:</mark>

Masquerading incoming traffic for specific destination: This is less common but possible.

It translates the source IP of incoming traffic destined for a specific server on your network to the masquerade IP.

```bash
iptables -t nat -A PREROUTING -i eth0 -d 192.168.1.20 -j MASQUERADE
```

### <mark style="color:purple;">REDIRECT</mark>

#### <mark style="color:green;">PREROUTING:</mark>

Forwarding external traffic to an internal server: Redirect traffic destined for a specific public port to a different port on an internal server.

{% code overflow="wrap" %}
```bash
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-destination 192.168.1.10:8080
```
{% endcode %}

Redirect all incoming traffic on port 80 to port 8080 on the local machine. (useful for transparent proxy)

```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
```

Redirecting DNS Queries to a Local DNS Server

```bash
iptables -t nat -A PREROUTING -p udp --dport 53 -j REDIRECT --to-port 5353
```

Redirecting traffic to port:

```bash
iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-port 8443
```

Redirecting Traffic for Multiple Ports:

```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 9999
iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-port 9999
```

Creating a Transparent SOCKS Proxy

If you have a SOCKS proxy running on port 1080 and you want to redirect specific outbound traffic to this proxy transparently, you could use the following setup.

Note that additional configuration on the SOCKS proxy might be required to handle the redirected traffic properly:

```bash
iptables -t nat -A PREROUTING -p tcp -d 192.168.100.0/24 -j REDIRECT --to-port 1080
```

Load balancing across internal servers: Distribute incoming traffic based on source IP or other criteria by redirecting to different ports on different servers.

{% code overflow="wrap" %}
```bash
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -m iprange --src-range 192.168.1.0/24 -j REDIRECT --to-destination 192.168.1.10:8080

iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -m iprange --src-range 192.168.1.128/24 -j REDIRECT --to-destination 192.168.1.20:8080
```
{% endcode %}

#### <mark style="color:green;">POSTROUTING:</mark>

Redirect outbound traffic to a local proxy server: This is less common but possible.

{% code overflow="wrap" %}
```bash
iptables -t nat -A POSTROUTING -o eth0 -p tcp --dport 80 -j REDIRECT --to-destination 192.168.1.25:8080
```
{% endcode %}

Localhost Traffic Redirection:

```bash
iptables -t nat -A OUTPUT -p tcp --dport 80 -o lo -j REDIRECT --to-port 8080
```

Redirecting to a Different Service Based on Source IP:

{% code overflow="wrap" %}
```bash
iptables -t nat -A PREROUTING -s 192.168.1.100 -p tcp --dport 80 -j REDIRECT --to-port 8080
```
{% endcode %}
