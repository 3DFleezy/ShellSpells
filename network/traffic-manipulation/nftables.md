# nftables

## <mark style="color:red;">Notes</mark>

### <mark style="color:purple;">Examples</mark>

{% code overflow="wrap" %}
```bash
sudo nft add table ip <RULE_NAME>

sudo nft add chain ip <RULE_NAME> FILTER { type filter hook input priority 0 \; policy accept \; }

sudo nft add rule ip <RULE_NAME> FILTER tcp sport {ssh, telnet, 3389, 6010-6050} ct state {new, established} accept

sudo nft list ruleset

sudo nft add chain ip <RULE_NAME> FILTER1 { type filter hook output priority 0 \; policy accept \; }

sudo nft list ruleset

sudo nft add rule ip <RULE_NAME> FILTER1 tcp sport {ssh, telnet, 3389, 6010-6050} ct state {new, established} accept

sudo nft add rule ip <RULE_NAME> FILTER tcp dport {ssh, telnet, 3389, 6010-6050} ct state {new, established} accept

sudo nft add rule ip <RULE_NAME> FILTER1 tcp dport {ssh, telnet, 3389, 6010-6050} ct state {new, established} accept
```
{% endcode %}

### <mark style="color:purple;">NFTable Families</mark>

ip - IPv4 packets

ip6 - IPv6 packets

inet - IPv4 and IPv6 packets

arp - layer 2

bridge - processing traffic/packets traversing bridges.

netdev - allows for user classification of packets - nftables passes up to the networking stack (no counterpart in iptables)

There are three chain types:

filter - to filter packets - can be used with arp, bridge, ip, ip6, and inet families

route - to reroute packets - can be used with ip and ipv6 families only

nat - used for Network Address Translation - used with ip and ip6 table families only

### <mark style="color:purple;">CREATION OF HOOKS</mark>

PREROUTING

POSTROUTING

INPUT

OUTPUT

FORWARD

INGRESS - used with NETDEV family only

## <mark style="color:red;">1. CREATE THE TABLE</mark>

nft add table \[family] \[table]

<table data-header-hidden data-full-width="true"><thead><tr><th width="178">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>[family]</code></mark></td><td>Represents the network protocol family such as ip, ip6, inet, arp, bridge, and netdev.</td></tr><tr><td><mark style="color:yellow;"><code>[table]</code></mark></td><td>Denotes a user-provided name for the table.</td></tr></tbody></table>

## <mark style="color:red;">2. CREATE THE BASE CHAIN</mark>

<mark style="color:yellow;">nft add chain \[family] \[table] \[chain] { type \[type] hook \[hook] priority \[priority] ; policy \[policy] ;}</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="187">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>[chain]</code></mark></td><td>User-defined name for the chain.</td></tr><tr><td><mark style="color:yellow;"><code>[type]</code></mark></td><td>Represents the type of chain, which can be filter, route, or nat.</td></tr><tr><td><mark style="color:yellow;"><code>[hook]</code></mark></td><td>Specifies the hook at which the chain should be activated, such as prerouting, ingress, input, forward, output, or postrouting.</td></tr><tr><td><mark style="color:yellow;"><code>[priority]</code></mark></td><td>User-provided integer representing the priority of the rule. Lower number indicates higher priority. Default is 0. Use "--" before negative numbers.</td></tr><tr><td><mark style="color:yellow;"><code>; [policy] ;</code></mark></td><td>Used to set the policy for the chain, which can be accept (default) or drop.</td></tr></tbody></table>

Use "" to escape the ";" in bash

## <mark style="color:red;">3. CREATE A RULE IN THE CHAIN</mark>

<mark style="color:yellow;">nft add rule \[family] \[table] \[chain] \[matches (matches)] \[statement]</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="184">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>[matches]</code></mark></td><td>Typically represents protocol headers (e.g., ip, ip6, tcp, udp, icmp, ether, etc.).</td></tr><tr><td><mark style="color:yellow;"><code>(matches)</code></mark></td><td>Refers to specific matches within the [matches] field.</td></tr><tr><td><mark style="color:yellow;"><code>[statement]</code></mark></td><td>Specifies the action performed when a packet is matched. Examples include log, accept, drop, reject, counter, nat (dnat, snat, masquerade).</td></tr></tbody></table>

## <mark style="color:red;">MODIFY NFTABLES</mark>

```bash
nft {list | flush} ruleset
nft {delete | list | flush } table [family] [table]
nft {delete | list | flush } chain [family] [table] [chain]
```

```bash
nft list table [family] [table] [-a]
```

Adds after position

{% code overflow="wrap" %}
```bash
nft add rule [family] [table] [chain] [position <position>] [matches (matches)] [statement]
```
{% endcode %}

Inserts before position

{% code overflow="wrap" %}
```bash
nft insert rule [family] [table] [chain] [position <position>] [matches (matches)] [statement]
```
{% endcode %}

Replaces rule at handle

{% code overflow="wrap" %}
```bash
nft replace rule [family] [table] [chain] [handle <handle>] [matches (matches)] [statement]
```
{% endcode %}

Deletes rule at handle

```bash
nft delete rule [family] [table] [chain] [handle <handle>]
```

## <mark style="color:red;">Save/Load nftables</mark>

Save the nftables rules:

```bash
nft list ruleset > /etc/nftables.configuration
```

Load the saved nftables configuration using the nft command:

```bash
nft -f /etc/nftables.conf
```

## <mark style="color:red;">Filter for SSH Traffic (Example)</mark>

### <mark style="color:purple;">Rules</mark>

Host A:

{% code overflow="wrap" %}
```bash
nft add table ip FILTER

nft add chain ip FILTER INPUT { type filter hook input priority 0 \; policy accept \;}

nft add chain ip FILTER OUTPUT { type filter hook output priority 0 \; policy accept \;}
```
{% endcode %}

Host B:

{% code overflow="wrap" %}
```bash
nft add table ip FILTER

nft add chain ip FILTER INPUT { type filter hook input priority 0 \; policy accept \;}

nft add chain ip FILTER OUTPUT { type filter hook output priority 0 \; policy accept \;}
```
{% endcode %}

Host A:

{% code overflow="wrap" %}
```bash
nft add rule ip FILTER OUTPUT tcp dport 22 ct state { new, established } accept
nft add rule ip FILTER INPUT tcp sport 22 ct state { new, established } accept
```
{% endcode %}

Host B:

{% code overflow="wrap" %}
```bash
nft add rule ip FILTER INPUT tcp dport 22 ct state { new, established } accept
nft add rule ip FILTER OUTPUT tcp sport 22 ct state { new, established } accept
```
{% endcode %}

Host A:

{% code overflow="wrap" %}
```bash
nft add rule ip FILTER INPUT tcp dport 22 ct state { new, established } accept
nft add rule ip FILTER OUTPUT tcp sport 22 ct state { new, established } accept
```
{% endcode %}

Host B:

{% code overflow="wrap" %}
```bash
nft add rule ip FILTER OUTPUT tcp dport 22 ct state { new, established } accept
nft add rule ip FILTER INPUT tcp sport 22  ct state { new, established } accept
```
{% endcode %}

Host A:

```bash
nft add chain ip FILTER INPUT { \; policy drop \;}
nft add chain ip FILTER OUTPUT { \; policy drop \;}
```

Host B:

```bash
nft add chain ip FILTER INPUT { \; policy drop \;}
nft add chain ip FILTER OUTPUT { \; policy drop \;}
```

## <mark style="color:red;">NAT, PAT, and NAT Port Forwarding (Examples)</mark>

Enable IP Forwarding:

```bash
Iecho 1 > /proc/sys/net/ipv4/ip_forward
```

```bash
nft add table ip NAT
nft add chain ip NAT PREROUTING { type nat hook prerouting priority 0 \; }
nft add chain ip NAT POSTROUTING { type nat hook postrouting priority 0 \; }
```

1-to-1 NAT (for the servers if you have extra IP's)

```bash
nft add rule ip NAT POSTROUTING oif eth0 ip saddr 10.0.0.10 snat to 100.1.1.10
nft add rule ip NAT POSTROUTING oif eth0 ip saddr 10.0.0.11 snat to 100.1.1.11
nft add rule ip NAT POSTROUTING oif eth0 ip saddr 10.0.0.12 snat to 100.1.1.12
```

PAT (for the clients)

```bash
nft add rule ip NAT POSTROUTING oif eth0 masquerade
```

Port Forward (for the servers if you don't have extra IP's)

```bash
nft add rule ip NAT PREROUTING iif eth0 tcp dport 80 dnat to 10.0.0.10:80
nft add rule ip NAT PREROUTING iif eth0 tcp dport 21 dnat to 10.0.0.11:21
nft add rule ip NAT PREROUTING iif eth0 tcp dport 23 dnat to 10.0.0.12:23
```
