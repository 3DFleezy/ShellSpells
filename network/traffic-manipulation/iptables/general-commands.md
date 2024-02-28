# General Commands

## <mark style="color:red;">Options</mark>

<table data-header-hidden><thead><tr><th width="119">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>-L</code></mark></td><td>List rules</td></tr><tr><td><mark style="color:yellow;"><code>-S</code></mark></td><td>List rules and commands used in the background</td></tr><tr><td><mark style="color:yellow;"><code>-A</code></mark></td><td>Append rule to bottom of list</td></tr><tr><td><mark style="color:yellow;"><code>-I</code></mark></td><td>Insert rule above rule specified</td></tr><tr><td><mark style="color:yellow;"><code>-R</code></mark></td><td>Replace specified rule</td></tr><tr><td><mark style="color:yellow;"><code>-P</code></mark></td><td>Policy (change policy)</td></tr><tr><td><mark style="color:yellow;"><code>-D</code></mark></td><td>Delete specified rule</td></tr><tr><td><mark style="color:yellow;"><code>-F</code></mark></td><td>Flush rules</td></tr></tbody></table>

## <mark style="color:red;">Match Statement Options</mark>

<table data-header-hidden><thead><tr><th width="120">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>-i</code></mark></td><td>Inbound interface</td></tr><tr><td><mark style="color:yellow;"><code>-o</code></mark></td><td>Outbound interface</td></tr><tr><td><mark style="color:yellow;"><code>-s</code></mark></td><td>Source IP</td></tr><tr><td><mark style="color:yellow;"><code>-d</code></mark></td><td>Destination IP</td></tr><tr><td><mark style="color:yellow;"><code>-p</code></mark></td><td>Protocol &#x3C;tcp/udp/icmp></td></tr><tr><td><mark style="color:yellow;"><code>-m</code></mark></td><td>Match &#x3C;multiport/state/conntrack/iprange></td></tr></tbody></table>

## <mark style="color:red;">List Rules</mark>

<table data-header-hidden><thead><tr><th width="493">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t [table] -L</code></mark></td><td>List rules in table</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t [table] -L &#x3C;chain> --line-numbers</code></mark></td><td>List rules in with line numbers</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t [table] -S</code></mark></td><td>List rules formatted as input for a script</td></tr></tbody></table>

## <mark style="color:red;">Check Rules</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="596">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t [table] -C &#x3C;chain> &#x3C;rule></code></mark></td><td>Check whether a specific rule exists</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t filter -C INPUT -p tcp --dport 80 -j ACCEPT</code></mark></td><td>Example</td></tr></tbody></table>

## <mark style="color:red;">Set Default Policy</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t [table] -P &#x3C;chain> &#x3C;action></code></mark></td><td>Set the default policy for the to</td></tr></tbody></table>

## <mark style="color:red;">Add/Replace Rules</mark>

<table><thead><tr><th width="437">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t [table] -A &#x3C;chain> &#x3C;specific rule></code></mark></td><td>Append rule to bottom of list</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t [table] -I &#x3C;chain> &#x3C;rule_num> &#x3C;rule></code></mark></td><td>Insert rule at specified rule number</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t [table] -R &#x3C;chain> &#x3C;rule_num> &#x3C;rule></code></mark></td><td>Replace rule at specified rule number</td></tr></tbody></table>

## <mark style="color:red;">Delete Specific Rules</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="622">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t [table] -D &#x3C;chain> [rule_num]</code></mark></td><td>Delete rule by number</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t filter -D INPUT -p tcp --dport 22 -j ACCEPT</code></mark></td><td>Delete specific rule</td></tr></tbody></table>

## <mark style="color:red;">Flush Rules</mark>

<table data-header-hidden><thead><tr><th width="359">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t [table] -F</code></mark></td><td>Flush all rules in [table]</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t [table] -F &#x3C;chain></code></mark></td><td>Flush all rules in in [table]</td></tr></tbody></table>

## <mark style="color:red;">Zero out the Packet and Byte Counters</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="449">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t [table] -Z</code></mark></td><td>Zero the packet and byte counters in all chains of the [table]</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t [table] -Z &#x3C;chain></code></mark></td><td>Zero the packet and byte counters in of the [table]</td></tr></tbody></table>

## <mark style="color:red;">Save/Restore iptables</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="529">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables-save -t [table] > /[table]_rules_backup</code></mark></td><td>Save the current iptables rules to a file</td></tr><tr><td><mark style="color:yellow;"><code>iptables-restore &#x3C; /[table]_rules_backup</code></mark></td><td>Restore iptables rules from a file</td></tr></tbody></table>

## <mark style="color:red;">Custom Chains</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="445">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>iptables -t [table] -N MYCHAIN</code></mark></td><td>Create custom chain MYCHAIN</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t [table] -X MYCHAIN</code></mark></td><td>Delete custom chain MYCHAIN (only if no references)</td></tr><tr><td><mark style="color:yellow;"><code>iptables -t [table] -E OLDCHAIN NEWCHAIN</code></mark></td><td>Rename chain from OLDCHAIN to NEWCHAIN</td></tr></tbody></table>

## <mark style="color:red;">RETURN Action</mark>

Exiting a user-defined chain and returning to the default processing flow.

This action is generally used within user-defined chains to stop processing and return to the calling chain.

```bash
iptables -t nat -N MYCHAIN
iptables -t nat -A MYCHAIN -s 192.168.1.0/24 -j RETURN
iptables -t nat -A PREROUTING -p tcp --dport 80 -j MYCHAIN
```

Here, the RETURN action in MYCHAIN stops further processing of packets from the 192.168.1.0/24 network and returns to the PREROUTING chain.

Basic Example with a User-defined Chain:

First, create a user-defined chain named CHECK\_HTTP and add a rule to it that logs HTTP traffic.

Then, use the RETURN action to return control to the calling chain after logging:

```bash
iptables -N CHECK_HTTP
iptables -A CHECK_HTTP -p tcp --dport 80 -j LOG --log-prefix "HTTP traffic: "
iptables -A CHECK_HTTP -j RETURN
iptables -A INPUT -p tcp --dport 80 -j CHECK_HTTP
```

This setup logs HTTP traffic and then returns to the INPUT chain for further processing.

Conditional Return Based on Source IP:

Imagine a scenario where you want to apply special processing to packets from a specific source IP, then return to the main chain if those conditions are met:

```bash
iptables -N SPECIAL_SOURCE
iptables -A SPECIAL_SOURCE -s 192.168.1.100 -j LOG --log-prefix "Special Source: "
iptables -A SPECIAL_SOURCE -j RETURN
iptables -A INPUT -j SPECIAL_SOURCE
```

Packets from 192.168.1.100 are logged, and then control returns to the INPUT chain.

Using RETURN in a Complex Filtering Scenario:

If you have complex filtering rules for different types of traffic, you might organize them into separate chains.

After specific conditions are checked in these chains, you might use RETURN to go back to a common set of rules:

```bash
iptables -N CHECK_SSH
iptables -A CHECK_SSH -p tcp --dport 22 -j LOG --log-prefix "SSH attempt: "
iptables -A CHECK_SSH -j RETURN
```

```bash
iptables -N CHECK_FTP
iptables -A CHECK_FTP -p tcp --dport 21 -j LOG --log-prefix "FTP attempt: "
iptables -A CHECK_FTP -j RETURN
```

```bash
iptables -A INPUT -p tcp --dport 22 -j CHECK_SSH
iptables -A INPUT -p tcp --dport 21 -j CHECK_FTP
iptables -A INPUT -j DROP
```

This setup logs SSH and FTP attempts before dropping all other incoming traffic.

Excluding Traffic from Broad Rules

If you want to apply a broad rule but exclude certain traffic from it, you could use RETURN to bypass the broad rule for specific cases:

```bash
iptables -N EXCLUDE_LOGGING
iptables -A EXCLUDE_LOGGING -s 192.168.1.200 -j RETURN
iptables -A EXCLUDE_LOGGING -j LOG --log-prefix "General logging: "
```

```bash
iptables -A INPUT -j EXCLUDE_LOGGING
```

Here, packets from 192.168.1.200 are not logged, thanks to the RETURN action that bypasses the logging rule for this source IP.

Combining RETURN with Rate Limiting

You can use RETURN to create a rate-limiting mechanism for specific types of traffic, returning control to the calling chain if the rate limit is not exceeded:

```bash
iptables -N RATE_LIMIT
iptables -A RATE_LIMIT -m limit --limit 1/min -j LOG --log-prefix "Rate limit: "
iptables -A RATE_LIMIT -j RETURN
iptables -A INPUT -p icmp -j RATE_LIMIT
```

This rule set logs up to one ICMP packet per minute and uses RETURN to continue processing other rules in the INPUT chain after applying rate limiting.
