# Mangle

## <mark style="color:red;">Mangle</mark>

### <mark style="color:purple;">Chains</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="177">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>PREROUTING</code></mark></td><td>Engaged for incoming packets before any routing decision is made, suitable for DNAT.</td></tr><tr><td><mark style="color:yellow;"><code>POSTROUTING</code></mark></td><td>Activated for outgoing packets after all routing decisions have been made, ideal for SNAT and masquerading.</td></tr><tr><td><mark style="color:yellow;"><code>OUTPUT</code></mark></td><td>Applied to locally generated packets before they are sent out, allowing for DNAT on outgoing traffic.</td></tr></tbody></table>

## <mark style="color:red;">Examples by Action</mark>

### <mark style="color:purple;">Custom TTL</mark>

```bash
sudo iptables -t mangle -A POSTROUTING -j TTL --ttl-set 128
```

Windows 128

Cisco 255

Linux 64

Increase TTL to prevent packets from expiring prematurely:

```bash
iptables -t mangle -A PREROUTING -i eth0 -j TTL --ttl-inc 64
```

Decrease TTL to restrict packet reach to a specific network segment:

```bash
iptables -t mangle -A POSTROUTING -o eth1 -d 192.168.2.0/24 -j TTL --ttl-set 32
```

This rule sets the TTL of outgoing packets destined for the 192.168.2.0/24 network to 32, limiting their reach to that segment.

### <mark style="color:purple;">Marking packets for differentiated treatment</mark>

Mark packets based on source IP for specific routing:

```bash
iptables -t mangle -A PREROUTING -i eth0 -s 192.168.1.10 -j MARK --set-mark 0x10
```

Mark packets based on destination port for specific firewall rules:

```bash
iptables -t mangle -A PREROUTING -i eth0 -p tcp --dport 80 -j MARK --set-mark 0x20
```

This marks packets targeting port 80 with 0x20 for applying specific firewall rules later.

### <mark style="color:purple;">Modifying packet flags</mark>

Disable timestamps on outgoing packets for performance optimization:

```bash
iptables -t mangle -A POSTROUTING -o eth0 -j TSOFF
```

Enable IP options for specific applications:

```bash
iptables -t mangle -A PREROUTING -i eth0 -p tcp --dport 443 -j TOS --set-tos 0x10
```

This sets the Type of Service (TOS) field for HTTPS traffic (port 443) to 0x10, potentially enabling specific options needed by the application.

Changing the DSCP Field of Outgoing Packets

Differentiated Services Code Point (DSCP) can be used for quality of service (QoS) purposes.

This rule sets the DSCP field for outgoing HTTP traffic to prioritize it within the network.

```bash
iptables -t mangle -A POSTROUTING -p tcp --dport 80 -j DSCP --set-dscp 32
```
