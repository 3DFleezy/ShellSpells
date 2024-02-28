# Syntax

## <mark style="color:red;">Syntax to Run TCPdump Against a PCAP with BPF:</mark>

```bash
tcpdump "yourfilter" -r BPFCheck.pcap
```

## <mark style="color:red;">BPF syntax with tcpdump</mark>

```bash
tcpdump protocol[byte#:size] {& mask} {operator} {value}
```

<table data-header-hidden data-full-width="true"><thead><tr><th width="175">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>protocol</code></mark></td><td>Identifies which header to look in. Mandatory. Can be ether, arp, ip, ip6, icmp, tcp, udp.</td></tr><tr><td><mark style="color:yellow;"><code>byte#</code></mark></td><td>Starting byte number to start looking. Mandatory. Can be from 0 to 20, etc.</td></tr><tr><td><mark style="color:yellow;"><code>size</code></mark></td><td>Identifies how many bytes to read. Optional. Can be 1 (default), 2, or 4.</td></tr><tr><td><mark style="color:yellow;"><code>&#x26; mask</code></mark></td><td>Bitwise mask used to specify specific bits. Optional. Can be in decimal or hex format.</td></tr><tr><td><mark style="color:yellow;"><code>operator</code></mark></td><td>Specifies the condition (=, &#x3C;, &#x3C;=, >, >=, !=) for the match. Mandatory.</td></tr><tr><td><mark style="color:yellow;"><code>value</code></mark></td><td>Identifies the value to match (or not match). Mandatory. Should be in the same format as the mask.</td></tr></tbody></table>

To conjoin 2 or more statements you can use = (<mark style="color:yellow;">`&&`</mark> or <mark style="color:yellow;">`and`</mark>), (<mark style="color:yellow;">`||`</mark> or <mark style="color:yellow;">`or`</mark>)

When using <mark style="color:yellow;">`&`</mark>, <mark style="color:yellow;">`&&`</mark>, <mark style="color:yellow;">`||`</mark>, and <mark style="color:yellow;">`( )`</mark> you must surround the entire statement with <mark style="color:yellow;">`" "`</mark> or <mark style="color:yellow;">`' '`</mark>

Remember that after every BPF statement must have an operator and a result to search for.

```bash
tcpdump {A} [B:C] {D} {E} {F} {G}
```

<mark style="color:yellow;">`A`</mark> = Protocol header (ether | arp | ip | ip6 | icmp | tcp | udp)

<mark style="color:yellow;">`B`</mark> = Header Byte offset

<mark style="color:yellow;">`C`</mark> = optional: Size in bytes. Can be 1 (byte), 2 (half-word) or 4 (word) (default 1 byte)

<mark style="color:yellow;">`D`</mark> = optional: Bitwise mask (&)

<mark style="color:yellow;">`E`</mark> = Operators = , == , > , < , <= , >= , != , () , << , >>

<mark style="color:yellow;">`F`</mark> = Value to search for

<mark style="color:yellow;">`G`</mark> = optional: Logical Operators and (&&) or or (||) to bridge expressions
