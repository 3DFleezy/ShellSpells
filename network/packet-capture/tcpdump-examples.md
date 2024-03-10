# TCPDump Examples

## <mark style="color:red;">General Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="364">Commands</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tcpdump -xx -r [pcapfile]</code></mark></td><td>Shows ASCII and hex from a file</td></tr><tr><td><mark style="color:yellow;"><code>tcpdump -i [interface]</code></mark></td><td>Capture on interface</td></tr></tbody></table>

## <mark style="color:red;">Simple</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="361">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ether</code></mark></td><td>Matches Ethernet headers.</td></tr><tr><td><mark style="color:yellow;"><code>arp</code></mark></td><td>Matches ARP packets.</td></tr><tr><td><mark style="color:yellow;"><code>icmp</code></mark></td><td>Matches ICMP packets.</td></tr><tr><td><mark style="color:yellow;"><code>ip</code></mark></td><td>Matches IPv4 packets.</td></tr><tr><td><mark style="color:yellow;"><code>ip6</code></mark></td><td>Matches IPv6 packets.</td></tr><tr><td><mark style="color:yellow;"><code>tcp</code></mark></td><td>Matches TCP packets.</td></tr><tr><td><mark style="color:yellow;"><code>udp</code></mark></td><td>Matches UDP packets.</td></tr><tr><td><mark style="color:yellow;"><code>host 192.168.1.1</code></mark></td><td>Matches packets arriving to or departing from the specified IP address.</td></tr><tr><td><mark style="color:yellow;"><code>net 192.168.1.0/24</code></mark></td><td>Matches packets arriving to or departing from the specified network.</td></tr><tr><td><mark style="color:yellow;"><code>tcp port 22</code></mark></td><td>Matches packets arriving to or departing from TCP port 22.</td></tr><tr><td><mark style="color:yellow;"><code>port 53</code></mark></td><td>Matches packets arriving to or departing from TCP or UDP port 53.</td></tr><tr><td><mark style="color:yellow;"><code>dst host 192.168.1.1</code></mark></td><td>Matches packets arriving to the specified IP address.</td></tr><tr><td><mark style="color:yellow;"><code>dst net 192.168.1.0/24</code></mark></td><td>Matches packets arriving to the specified network.</td></tr><tr><td><mark style="color:yellow;"><code>tcp dst port 22</code></mark></td><td>Matches packets arriving to TCP port 22.</td></tr><tr><td><mark style="color:yellow;"><code>src host 192.168.1.1</code></mark></td><td>Matches packets departing from the specified IP address.</td></tr><tr><td><mark style="color:yellow;"><code>src net 192.168.1.0/24</code></mark></td><td>Matches packets departing from the specified network.</td></tr><tr><td><mark style="color:yellow;"><code>tcp src port 22</code></mark></td><td>Matches packets departing from TCP port 22.</td></tr><tr><td><mark style="color:yellow;"><code>tcp[tcpflags] = tcp-ack</code></mark></td><td>Matches TCP packets with the ACK flag set.</td></tr><tr><td><mark style="color:yellow;"><code>'icmp[icmptype] = icmp-echo'</code></mark></td><td>Matches ICMP echo-request packets.</td></tr><tr><td><mark style="color:yellow;"><code>'icmp[icmptype] = icmp-reply'</code></mark></td><td>Matches ICMP echo-reply packets.</td></tr></tbody></table>

## <mark style="color:red;">Complex</mark>

Traffic between 192.168.1.1 and either 10.1.1.1 or 10.1.1.2:

```bash
host 192.168.1.1 and \( 10.1.1.1 or 10.1.1.2 \)
```

All IP packets between 10.1.1.1 and any host except 10.1.1.2:

```bash
ip host 10.1.1.1 and not 10.1.1.2
```

All traffic between local hosts and hosts at Berkeley:

```bash
net ucb-ether
```

All ftp traffic through internet gateway 192.168.1.1:

```bash
'gateway 192.168.1.1 and (port ftp or ftp-data)'
```

No traffic TO or FROM local network:

```bash
ip and not net localnet
```

The start and end packets (the SYN and FIN packets) of each TCP conversation that involves a non-local host:

```bash
'tcp[tcpflags] & (tcp-syn|tcp-fin) != 0 and not src and dst net localnet'
```

TCP packets with flags RST and ACK both set. (i.e. select only the RST and ACK flags in the flags field, and if the result is "RST and ACK both set", match):

```bash
'tcp[tcpflags] & (tcp-rst|tcp-ack) == (tcp-rst|tcp-ack)'
```

All IPv4 HTTP packets to and from port 80. Prints only packets that contain data:

```bash
'tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)'
```

IP packets longer than 576 bytes sent through gateway 192.168.1.1:

```bash
'gateway 192.168.1.1 and ip[2:2] > 576'
```

IP broadcast or multicast packets that were not sent via Ethernet broadcast or multicast:

```bash
'ether[0] & 1 = 0 and ip[16] >= 224'
```

All ICMP packets that are not echo requests/replies (i.e., not ping packets):

```bash
'icmp[icmptype] != icmp-echo and icmp[icmptype] != icmp-echoreply'
```

## <mark style="color:red;">Specific Examples</mark>

<mark style="color:orange;">HTTP</mark> traffic:

```bash
tcp[2:2]=80||tcp[0:2]=80
```

<mark style="color:orange;">TELNET</mark> traffic:

```bash
tcp[2:2]=23 || tcp[0:2]=23
```

<mark style="color:orange;">ARP</mark> traffic:

```bash
ether[12:2]=0x0806
```

<mark style="color:orange;">IPv4</mark> packets relating to <mark style="color:orange;">DNS</mark>:

```bash
tcp[0:2]=53 || tcp[2:2]=53 || udp[0:2]=53 || udp[2:2]=53
```

<mark style="color:orange;">IP</mark> packets with a <mark style="color:orange;">TTL</mark> of 64 or less:

```bash
ip[8]<=64 || ip6[7]<=64
```

<mark style="color:orange;">IPv4</mark> packets with at least the <mark style="color:orange;">Dont Fragment Bit</mark>set:

```bash
ip[6] & 64 = 64
```

<mark style="color:orange;">Source Port</mark> higher than 1024, using Transport Layer headers:

```bash
tcp[0:2]>1024 || udp[0:2]>1024	
```

<mark style="color:orange;">UDP</mark> packets, utilizing the <mark style="color:orange;">IPv4</mark> or <mark style="color:orange;">IPv6</mark> Headers:

```bash
ip[9]=17 || ip6[6]=17	
```

<mark style="color:orange;">ACK/RST</mark> or <mark style="color:orange;">ACK/FIN</mark> flag set, utilizing the correct Transport Layer Header:

```bash
tcp[13] = 20 || tcp[13]=17
```

<mark style="color:orange;">IP ID</mark> field of 213:

```bash
ip[4:2]=213
```

<mark style="color:orange;">VLAN</mark> tags:

```bash
ether[12:2]=0x8100
```

Initial packets from a <mark style="color:orange;">client initiating a TCP connection</mark>:

```bash
tcp[13]=2
```

<mark style="color:orange;">RESPONSE</mark> packets from a server listening on an <mark style="color:orange;">open</mark> TCP port:

```bash
tcp[13]=18
```

<mark style="color:orange;">RESPONSE packets from a server</mark> with <mark style="color:orange;">closed</mark> TCP ports:

```bash
tcp[13]=4
```

<mark style="color:orange;">TCP</mark> and <mark style="color:orange;">UDP</mark> packets sent to <mark style="color:orange;">well known ports</mark>:

```bash
tcp[2:2]<=1023 || udp[2:2]<=1023
```

<mark style="color:orange;">Evil bit</mark> is set:

```bash
ip[6]=128
```

<mark style="color:orange;">CHAOS</mark> protocol within an IPv4 header:

```bash
ip[9]=16
```

<mark style="color:orange;">DSCP</mark> field of 37, IP packets:

```bash
ip[1] >> 2 = 37
```

<mark style="color:orange;">URG</mark> flag is not set and URG pointer has a value:

```bash
tcp[13]!=32 && tcp[18:2]>0
tcp[13]&32=0&&tcp[18:2]!=0
```

TCP <mark style="color:orange;">null scan</mark> to the host 10.10.10.10:

```bash
ip[16:4]=0x0a0a0a0a && tcp[13]=0
```

Attacker using <mark style="color:orange;">VLAN hopping</mark> to move from vlan 1 to vlan 10:

```bash
ether[12:4]& 0xFFFF0FFF = 0x81000001 && ether[16:4]& 0xFFFF0FFF = 0x8100000a
```

<mark style="color:orange;">IPv4</mark> packets targeting just the beginning of potential traceroutes as it's entering your network.

This can be from a Windows or Linux machine using their default settings.

Understan the default carrier protocols used by Windows vs Linux:

```bash
(ip[9]=1 && ip[8]=1) || (ip[9]=17 && ip[8]=1)
(ip[8]=1&&ip[9]=1)||(ip[8]=1&&ip[9]=17)
```

## <mark style="color:red;">Ethernet Header</mark>

```bash
Ether Type 	Type of Traffic
0x0800		IPv4
0x0806		ARP
0x86DD 		IPv6
0x8100		VLAN Tag
```

Destination MAC (read first 4 bytes then last 2). Although possible with BPF's its recommended to use primatives:

```bash
'ether[0:4] & 0xFFFFFFFF && ether[4:2] = 0xFFFF' 
```

OUI part of the MAC (reads first 4 bytes but ignores value in 4th byte):

```bash
'ether[0:4] & 0xFFFFFF00 = 0xFFFFFFFF' 
```

Source MAC (read first 4 bytes then last 2) Although possibel with BPF's its recommended to use primatives:

```bash
'ether[6:4] & 0xFFFFFFFF && ether[10:2] = 0xFFFF'
```

Ether-Type field (Here you will specify the Hex Ethertype you are searching for)

```bash
ether[12:2] = 0x800
```

```bash
'ether[0:4] = 0xfa163ef0 && ether[4:2] = 0xcafc'
'ether[0] & 0x01 = 0x01 || ether[6] & 0x01 = 0x01'
'ether[0] & 0x01 = 0x00 || ether[6] & 0x01 = 0x00'
'ether[0] & 0x02 = 0x02 || ether[6] & 0x02 = 0x02'
'ether[0] & 0x02 = 0x00 || ether[6] & 0x02 = 0x00'
'ether[6:4] = 0xffffffff && ether[10:2] = 0xffff'
'ether[12:2] = 0x0800 || ether[12:2] = 0x0806 || ether[12:2] = 0x86dd'
```

## <mark style="color:red;">VLAN Header</mark>

VLAN Ether type and then the VLAN Tag. <mark style="color:orange;">`xxx`</mark> will be the VLAN number in Hex.

This will search for 0x8100 (VLAN Tag) Ethertype.

Then search for the 12-bit VLAN number in Hex or Decimal.

This will ignore the 4-bit PCP/DEI field.

```bash
'ether[12:2] = 0x8100 && ether[14:2] & 0x0fff = 0x0xxx'
```

VLAN ID and Tag (at same time) <mark style="color:orange;">`xxx`</mark> will be the VLAN number in Hex.

This will perform the same task as above. This only combines the search fields.

It masks the E-type field and VLAN ID field while ignoring the PCP/DEI field.

```bash
'ether[12:4] & 0xffff0fff = 0x81000xxx'
```

Encapsulated VLAN frames that carey either IPv4, ARP, or IPv6 traffic.

{% code overflow="wrap" %}
```bash
'ether[12:2] = 0x8100 && (ether[16:2] = 0x0800 || ether[16:2] = 0x0806 || ether[16:2] = 0x86dd)'
```
{% endcode %}

Double Tagged:

```bash
'ether[12:4] & 0xffff0fff = 0x81000001 && ether[16:4] & 0xffff0fff = 0x81000064'
```

## <mark style="color:red;">ARP Header</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="510">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>arp[0:2] =</code></mark></td><td>Hardware Type</td></tr><tr><td><mark style="color:yellow;"><code>arp[2:2] =</code></mark></td><td>Protocol Type</td></tr><tr><td><mark style="color:yellow;"><code>arp[4] =</code></mark></td><td>Hardware Length</td></tr><tr><td><mark style="color:yellow;"><code>arp[5] =</code></mark></td><td>Protocol Length</td></tr><tr><td><mark style="color:yellow;"><code>arp[6:2] =</code></mark></td><td>Opcode</td></tr><tr><td><mark style="color:yellow;"><code>arp[16:4] =</code></mark></td><td>Sender IP</td></tr><tr><td><mark style="color:yellow;"><code>arp[24:4] =</code></mark></td><td>Destination IP</td></tr><tr><td><mark style="color:yellow;"><code>'arp[8:4] &#x26; 0xFFFFFFFF &#x26;&#x26; arp[12:2] = 0xFFFF'</code></mark></td><td>Sender MAC (read first 4 bytes then last 2)</td></tr><tr><td><mark style="color:yellow;"><code>'arp[18:4] &#x26; 0xFFFFFFFF &#x26;&#x26; arp[22:2] = 0xFFFF'</code></mark></td><td>Destination MAC (read first 4 bytes then last 2)</td></tr></tbody></table>

## <mark style="color:red;">IPv4 Header</mark>

### <mark style="color:purple;">All Fields</mark>

<table data-header-hidden><thead><tr><th width="263">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ip[0] &#x26; 0xf0 =</code></mark></td><td>IP version (hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[0] &#x26; 240 =</code></mark></td><td>IP Version (decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[0] 0x0f =</code></mark></td><td>Header Length in 4 octet words. Should be 5. (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[0] &#x26; 15 =</code></mark></td><td>Header Length in 4 octet words. Should be 5. (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[1] =</code></mark></td><td>Type of Service (TOS)</td></tr><tr><td><mark style="color:yellow;"><code>ip[1] &#x26; 0xfc =</code></mark></td><td>DSCP field only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[1] &#x26; 252 =</code></mark></td><td>DSCP field only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[1] &#x26; 0x03 =</code></mark></td><td>ECN field only. (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[1] &#x26; 3 =</code></mark></td><td>ECN field only. (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[2:2] =</code></mark></td><td>Total length of datagram in octets.</td></tr><tr><td><mark style="color:yellow;"><code>ip[4:2] =</code></mark></td><td>IP ID number</td></tr><tr><td><mark style="color:yellow;"><code>ip[6] &#x26; 0xE0 =</code></mark></td><td>Entire 3-bit flag field (RES, DF, MF). (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6] &#x26; 224 =</code></mark></td><td>Entire 3-bit flag field (RES, DF, MF). (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6] &#x26; 0x80 =</code></mark></td><td>Reserved bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6] &#x26; 128 =</code></mark></td><td>Reserved bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6] &#x26; 0x40 =</code></mark></td><td>Don't Fragment (DF) flag only. (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6] &#x26; 64 =</code></mark></td><td>Don't Fragment (DF) flag only. (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6] &#x26; 0x20 =</code></mark></td><td>MF flag only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6] &#x26; 32 =</code></mark></td><td>MF flag only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6:2] &#x26; 0x1FFF =</code></mark></td><td>Fragment Offset field (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6:2] &#x26; 8191 =</code></mark></td><td>Fragment Offset field (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip[6:2] =</code></mark></td><td>Entire Flags and Fragment Offset field</td></tr><tr><td><mark style="color:yellow;"><code>ip[8] =</code></mark></td><td>TTL</td></tr><tr><td><mark style="color:yellow;"><code>ip[9] =</code></mark></td><td>Protocol</td></tr><tr><td><mark style="color:yellow;"><code>ip[10:2] =</code></mark></td><td>Header Checksum</td></tr><tr><td><mark style="color:yellow;"><code>ip[12:4] =</code></mark></td><td>Source IP (Should be expressed in Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[16:4] =</code></mark></td><td>Destination IP (Should be expressed in Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip[20..60] =</code></mark></td><td>If any options.</td></tr></tbody></table>

### <mark style="color:purple;">Flag Bits</mark>

<table data-header-hidden><thead><tr><th width="191">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>'ip[6] = 128'</code></mark></td><td>Byte 6 can ONLY have the <mark style="color:orange;">RES</mark> bit on. No other bits can be set.</td></tr><tr><td><mark style="color:yellow;"><code>'ip[6] = 64'</code></mark></td><td>Byte 6 can ONLY have the <mark style="color:orange;">DF</mark> bit on. No other bits can be set.</td></tr><tr><td><mark style="color:yellow;"><code>'ip[6] = 32'</code></mark></td><td>Byte 6 can ONLY have the <mark style="color:orange;">MF</mark> bit on. No other bits can be set.</td></tr></tbody></table>

The high 3 bits of byte 6 are checked. The remaining 5 bits are not checked.

High 3 bits can only have the <mark style="color:orange;">DF</mark> bit set. Other 2 bits MUST be off. Remaining 5 bits are ignored.

```bash
'ip[6] & 0xE0 = 0x40'
'ip[6] & 224 = 64'	
```

The high 3 bits of byte 6 are checked. The remaining 5 bits are not checked.

High 3 bits can only have the <mark style="color:orange;">MF</mark> bit set. Other 2 bits MUST be off. Remaining 5 bits are ignored.

```bash
'ip[6] & 0xE0 = 0x20'
'ip[6] & 224 = 32'	
```

Only the <mark style="color:orange;">RES</mark> bit is checked and MUST be <mark style="color:orange;">ON</mark>. All other bits in byte 6 are ignored.

```bash
'ip[6] & 0x80 = 0x80'
'ip[6] & 128 = 128'	
```

Only the <mark style="color:orange;">RES</mark> bit is checked and MUST be <mark style="color:orange;">OFF</mark>. All other bits in byte 6 are ignored.

```bash
'ip[6] & 0x80 = 0x0'
'ip[6] & 128 = 0'	
```

Only the <mark style="color:orange;">DF</mark> bit is checked and MUST be <mark style="color:orange;">ON</mark>. All other bits in byte 6 are ignored.

```bash
'ip[6] & 0x40 = 0x40'
'ip[6] & 64 = 64'	
```

Only the <mark style="color:orange;">DF</mark> bit is checked and MUST be <mark style="color:orange;">OFF</mark>. All other bits in byte 6 are ignored.

```bash
'ip[6] & 0x40 = 0x0'
'ip[6] & 64 = 0'	
```

Only the <mark style="color:orange;">MF</mark> bit is checked and MUST be <mark style="color:orange;">ON</mark>. All other bits in byte 6 are ignored.

```bash
'ip[6] & 0x20 = 0x20'
'ip[6] & 32 = 32'	
```

Only the <mark style="color:orange;">MF</mark> bit is checked and MUST be <mark style="color:orange;">OFF</mark>. All other bits in byte 6 are ignored.

```bash
'ip[6] & 0x20 = 0x0'
'ip[6] & 32 = 0'	
```

### <mark style="color:purple;">TTLs</mark>

#### <mark style="color:green;">Default TTL's:</mark>

Windows = 128

Linux = 64

Cisco = 255

```bash
ip[8] = 255
ip[8] < 255
ip[8] <= 255
ip[8] <= 64 || ip[8] > 40'
ip[8] <= 128 || ip[8] > 100'
```

### <mark style="color:purple;">Protocols</mark>

ICMPv4 = 0x01 or 1

TCP = 0x06 or 6

UDP = 0x11 or 17

For more, see IANA protocol numbers

| <mark style="color:yellow;">`'ip[9] = 0x01'`</mark> | ICMPv4 |
| --------------------------------------------------- | ------ |
| <mark style="color:yellow;">`'ip[9] = 0x06'`</mark> | TCP    |
| <mark style="color:yellow;">`'ip[9] = 0x11'`</mark> | UDP    |

```bash
'ip[9] = 1 || ip[9] = 6 || ip[9] = 17' 	
```

### <mark style="color:purple;">Source/Destination IPs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="524">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>'ip[12:4] = 0x0a0a0a0a'</code></mark></td><td>Source IP</td></tr><tr><td><mark style="color:yellow;"><code>'ip[16:4] = 0x0a0a0a0a'</code></mark></td><td>Destination IP</td></tr><tr><td><mark style="color:yellow;"><code>'ip[12:4] = 0x0a0a0a0a || ip[16:4] = 0x0a0a0a0a'</code></mark></td><td>Both</td></tr></tbody></table>

### <mark style="color:purple;">IP Version and Header Length (IHL)</mark>

```bash
'ip[0] = 0x45'
'ip[0] & 0xf0= 0x40'
'ip[0] & 0x0f= 0x05'
'ip[0] & 0x0f > 0x05'
'ip[0] & 15 > 5'
```

### <mark style="color:purple;">All with MF (More Flags) Flag Set OR Has An Offset Value Greater Than Zero</mark>

```bash
'ip[6] & 0x20 = 0x20 || ip[6:2] & 0x1fff > 0'
'ip[6] & 32 = 32 || ip[6:2] & 8191 > 0'
'ip[6:2] & 0x1fff = 999'
```

## <mark style="color:red;">IPv6 Header</mark>

### <mark style="color:purple;">All</mark>

<table data-header-hidden><thead><tr><th width="293">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ip6[0] &#x26; 0xf0 =</code></mark></td><td>IP version (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>ip6[0] &#x26; 240 =</code></mark></td><td>IP version (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>ip6[0:2] &#x26; 0x0ff0 =</code></mark></td><td>Traffic Class Field</td></tr><tr><td><mark style="color:yellow;"><code>ip6[0:4] &#x26; 0x000fffff =</code></mark></td><td>Flow Label Field</td></tr><tr><td><mark style="color:yellow;"><code>ip6[4:2] =</code></mark></td><td>Payload length</td></tr><tr><td><mark style="color:yellow;"><code>ip6[6] =</code></mark></td><td>Next Header</td></tr><tr><td><mark style="color:yellow;"><code>ip6[7] =</code></mark></td><td>Hop limit (TTL)</td></tr></tbody></table>

### <mark style="color:purple;">Next Header</mark>

```bash
ip6[6] = 0x3a
ip6[6] = 0x06
ip6[6] = 0x11
```

```bash
'ip6[6] = 0x06 || ip6[6] = 0x11'
```

### <mark style="color:purple;">Hop Limit (TTL)</mark>

```bash
ip6[7] = 255
```

## <mark style="color:red;">ICMP Header</mark>

<table data-header-hidden><thead><tr><th width="196">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>icmp[0] =</code></mark></td><td>ICMP type</td></tr><tr><td><mark style="color:yellow;"><code>icmp[1] =</code></mark></td><td>ICMP code</td></tr><tr><td><mark style="color:yellow;"><code>icmp[2:2] =</code></mark></td><td>Checksum</td></tr><tr><td><mark style="color:yellow;"><code>icmp[4...] =</code></mark></td><td>Payload</td></tr></tbody></table>

```bash
'icmp[0] = 0 || icmp[0]=8'
'icmp[0]=3 && icmp[1]=3'
```

Notable control messages: https://en.wikipedia.org/wiki/Internet\_Control\_Message\_Protocol

## <mark style="color:red;">TCP Header</mark>

### <mark style="color:purple;">All</mark>

<table data-header-hidden><thead><tr><th width="237">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tcp[0:2] =</code></mark></td><td>16-bit Source Port</td></tr><tr><td><mark style="color:yellow;"><code>tcp[2:2] =</code></mark></td><td>16-bit Destination Port</td></tr><tr><td><mark style="color:yellow;"><code>tcp[4:4] =</code></mark></td><td>32-bit Sequence Number</td></tr><tr><td><mark style="color:yellow;"><code>tcp[8:4] =</code></mark></td><td>32-bit Ack Number</td></tr><tr><td><mark style="color:yellow;"><code>tcp[12] =</code></mark></td><td>Header Length</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] =</code></mark></td><td>Whole TCP Flags Field</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 0x80 =</code></mark></td><td>CWR bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 128 =</code></mark></td><td>CWR bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 0x40 =</code></mark></td><td>ECE bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 64 =</code></mark></td><td>ECE bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 0x20 =</code></mark></td><td>URG bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 32 =</code></mark></td><td>URG bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 0x10 =</code></mark></td><td>ACK bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 16 =</code></mark></td><td>ACK bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 0x08 =</code></mark></td><td>PSH bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 8 =</code></mark></td><td>PSH bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 0x04 =</code></mark></td><td>RST bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 4=</code></mark></td><td>RST bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 0x02 =</code></mark></td><td>SYN bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 2 =</code></mark></td><td>SYN bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 0x01 =</code></mark></td><td>FIN bit only (Hex)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[13] &#x26; 1 =</code></mark></td><td>FIN bit only (Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>tcp[14:2] =</code></mark></td><td>Window Size</td></tr><tr><td><mark style="color:yellow;"><code>tcp[16:2] =</code></mark></td><td>Checksum</td></tr><tr><td><mark style="color:yellow;"><code>tcp[18:2] =</code></mark></td><td>Urgent Pointer</td></tr><tr><td><mark style="color:yellow;"><code>tcp[20...60] =</code></mark></td><td>Options or data (if any)</td></tr></tbody></table>

### <mark style="color:purple;">Flags</mark>

```bash
128	64	32	16	8	4	2	1
CWR	ECE	URG	ACK	PSH	RST	SYN	FIN
```

### Examples:

#### <mark style="color:green;">Very Specific:</mark>

Only packets with the ACK+PSH flags set and NO other flags.

```bash
tcp[13] = 24
```

#### <mark style="color:green;">Less Specific:</mark>

Any packets with the ACK+PSH flags set and other flags are ignored.

```bash
tcp [13] & 24 = 24
```

Any packets with the ACK flags set and the PSH flag not set. Other flags are ignored.

```bash
tcp [13] & 24 = 16
```

#### <mark style="color:green;">Least Specific:</mark>

Packets that have the ACK and/or PSH set but NOT both off. Other flags are ignored.

```bash
tcp[13] & 24 !=0
```

### <mark style="color:purple;">Window Sizes</mark>

<pre class="language-bash"><code class="lang-bash">Operating system		TTL		TCP Window Size
Linux (Kernel 2.4 and 2.6)	64		5840
Google Linux			64		5720
FreeBSD				64		65535
Win XP			        128 	        65535
<strong>Win Vista and 7 (Server 2008) 	128		8192
</strong>iOS 12.4 (Cisco Routers)	255		4128
</code></pre>

## <mark style="color:red;">UDP Header</mark>

<table data-header-hidden><thead><tr><th width="357">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>udp[0:2] =</code></mark></td><td>16-bit source port (Specify in Hex or Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>udp[2:2] =</code></mark></td><td>16-bit destination port (Specify in Hex or Decimal)</td></tr><tr><td><mark style="color:yellow;"><code>udp[4:2] =</code></mark></td><td>Datagram Length</td></tr><tr><td><mark style="color:yellow;"><code>udp[6:2] =</code></mark></td><td>UDP Checksum</td></tr><tr><td><mark style="color:yellow;"><code>'udp[0:2]=69'</code></mark></td><td>Source Port</td></tr><tr><td><mark style="color:yellow;"><code>'udp[2:2]=69'</code></mark></td><td>Destination Port</td></tr><tr><td><mark style="color:yellow;"><code>'udp[0:2] = 53 || udp[2:2]=53'</code></mark></td><td>Source OR Dest Port</td></tr><tr><td><mark style="color:yellow;"><code>'ip[6:2] &#x26; 0x3fff != 0'</code></mark></td><td>UDP Checksum</td></tr></tbody></table>
