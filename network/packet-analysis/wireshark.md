# Wireshark

```bash
{ ether | arp | ip | icmp | tcp | udp }

{ bootp | dns | smtp | imap | pop | ftp | ftp-data | malformed }

ip.addr == x.x.x.x

!(ip.addr == x.x.x.x)

ip.addr == x.x.x.x && ip.addr == x.x.x.x

ip.addr >= x.x.x.x and ip.addr <= x.x.x.x

ip.src == xxxx && ip.dst == xxxx

tcp.port==xxx

!(tcp.port==xxx)

udp.port==xxx

tcp.dstport == xx

tcp.srcport == xx

tcp.flags.reset==1

tcp.flags.push == 1

{ip | tcp | udp | data } contains "xxx"

http or https

http.request

http.request.method == "GET"

http.request.method == "POST"
```
