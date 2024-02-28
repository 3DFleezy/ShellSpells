# Filter for SSH Traffic (Example)

## <mark style="color:red;">Precaution Command Before DROP Policy (LAB)</mark>

Do this before you change the policy in a LAB ENVIRONMENT to ensure that you do not lock yourself out of the box:

#### <mark style="color:green;">Before changing the policy to DROP</mark>

run the following command:

```bash
sudo shutdown -r 5
```

This will tell the system to reboot <mark style="color:yellow;">`-r`</mark> in 5 minutes

#### <mark style="color:green;">Change your policy to DROP</mark>

```bash
iptables -t filter -P INPUT DROP
iptables -t filter -P OUTPUT DROP
iptables -t filter -P FORWARD DROP
```

If changing the policy to DROP locked you out of your system then the system will reboot within 5 minutes which will clear out your rules.

If you did not get locked out, then run the following command to cancel the reboot:

```bash
sudo shutdown -c
```

## <mark style="color:red;">Examples</mark>

### <mark style="color:purple;">Without using Multiport</mark>

Host A:

{% code overflow="wrap" %}
```bash
iptables -t filter -A OUTPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT

iptables -t filter -A INPUT -p tcp --sport 22 -m state --state NEW,ESTABLISHED -j ACCEPT

iptables -t filter -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT

iptables -t filter -A OUTPUT -p tcp --sport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
```
{% endcode %}

Host B:

{% code overflow="wrap" %}
```bash
iptables -t filter -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT

iptables -t filter -A OUTPUT -p tcp --sport 22 -m state --state NEW,ESTABLISHED -j ACCEPT

iptables -t filter -A OUTPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT

iptables -t filter -A INPUT -p tcp --sport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
```
{% endcode %}

### <mark style="color:purple;">Using Multiport</mark>

Host A:

{% code overflow="wrap" %}
```bash
iptables -t filter -A INPUT -p tcp -m multiport --ports 22 -m state --state NEW,ESTABLISHED -j ACCEPT

iptables -t filter -A OUTPUT -p tcp -m multiport --ports 22 -m state --state NEW,ESTABLISHED -j ACCEPT
```
{% endcode %}

Host B:

{% code overflow="wrap" %}
```bash
iptables -t filter -A INPUT -p tcp -m multiport --ports 22 -m state --state NEW,ESTABLISHED -j ACCEPT

iptables -t filter -A OUTPUT -p tcp -m multiport --ports 22 -m state --state NEW,ESTABLISHED -j ACCEPT
```
{% endcode %}

## <mark style="color:red;">NAT, PAT, and Port Forward (Examples)</mark>

Enable IP Forwarding:

```bash
| echo 1 > /proc/sys/net/ipv4/ip_forward
```

1-to-1 NAT (for the servers if you have extra IP's)

```bash
iptables -t nat -A POSTROUTING -o eth0 -s 10.0.0.10 -j SNAT --to 100.1.1.10
iptables -t nat -A POSTROUTING -o eth0 -s 10.0.0.11 -j SNAT --to 100.1.1.11
iptables -t nat -A POSTROUTING -o eth0 -s 10.0.0.12 -j SNAT --to 100.1.1.12
```

PAT (for the clients)

```bash
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

Port Forward (for the servers if you don't have extra IP's)

```bash
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 10.0.0.10:80
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 21 -j DNAT --to 10.0.0.11:21
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 23 -j DNAT --to 10.0.0.12:23
```
