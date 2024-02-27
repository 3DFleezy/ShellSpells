# General Commands

## <mark style="color:red;">Options</mark>

| Command                                 | Description                                    |
| --------------------------------------- | ---------------------------------------------- |
| <mark style="color:yellow;">`-L`</mark> | List rules                                     |
| <mark style="color:yellow;">`-S`</mark> | List rules and commands used in the background |
| <mark style="color:yellow;">`-A`</mark> | Append rule to bottom of list                  |
| <mark style="color:yellow;">`-I`</mark> | Insert rule above rule specified               |
| <mark style="color:yellow;">`-R`</mark> | Replace specified rule                         |
| <mark style="color:yellow;">`-P`</mark> | Policy (change policy)                         |
| <mark style="color:yellow;">`-D`</mark> | Delete specified rule                          |
| <mark style="color:yellow;">`-F`</mark> | Flush rules                                    |

## <mark style="color:red;">Match Statement Options</mark>

| Command                                 | Description                                |
| --------------------------------------- | ------------------------------------------ |
| <mark style="color:yellow;">`-i`</mark> | Inbound interface                          |
| <mark style="color:yellow;">`-o`</mark> | Outbound interface                         |
| <mark style="color:yellow;">`-s`</mark> | Source IP                                  |
| <mark style="color:yellow;">`-d`</mark> | Destination IP                             |
| <mark style="color:yellow;">`-p`</mark> | Protocol \<tcp/udp/icmp>                   |
| <mark style="color:yellow;">`-m`</mark> | Match \<multiport/state/conntrack/iprange> |

## <mark style="color:purple;">List Rules</mark>

| Command                                                                            | Description                                |
| ---------------------------------------------------------------------------------- | ------------------------------------------ |
| <mark style="color:yellow;">`iptables -t [table] -L`</mark>                        | List rules in table                        |
| <mark style="color:yellow;">`iptables -t [table] -L <chain> --line-numbers`</mark> | List rules in with line numbers            |
| <mark style="color:yellow;">`iptables -t [table] -S`</mark>                        | List rules formatted as input for a script |

### <mark style="color:purple;">Check Rules</mark>

| Command                                                                                      | Description                          |
| -------------------------------------------------------------------------------------------- | ------------------------------------ |
| <mark style="color:yellow;">`iptables -t [table] -C <chain> <rule>`</mark>                   | Check whether a specific rule exists |
| <mark style="color:yellow;">`iptables -t filter -C INPUT -p tcp --dport 80 -j ACCEPT`</mark> | Example                              |

### <mark style="color:purple;">Set Default Policy</mark>

| Command                                                                      | Description                       |
| ---------------------------------------------------------------------------- | --------------------------------- |
| <mark style="color:yellow;">`iptables -t [table] -P <chain> <action>`</mark> | Set the default policy for the to |

### <mark style="color:purple;">Add/Replace Rules</mark>

| Command                                                                               | Description                           |
| ------------------------------------------------------------------------------------- | ------------------------------------- |
| <mark style="color:yellow;">`iptables -t [table] -A <chain> <specific rule>`</mark>   | Append rule to bottom of list         |
| <mark style="color:yellow;">`iptables -t [table] -I <chain> <rule_num> <rule>`</mark> | Insert rule at specified rule number  |
| <mark style="color:yellow;">`iptables -t [table] -R <chain> <rule_num> <rule>`</mark> | Replace rule at specified rule number |

### <mark style="color:purple;">Delete Specific Rules</mark>

| Command                                                                                      | Description           |
| -------------------------------------------------------------------------------------------- | --------------------- |
| <mark style="color:yellow;">`iptables -t [table] -D <chain> [rule_num]`</mark>               | Delete rule by number |
| <mark style="color:yellow;">`iptables -t filter -D INPUT -p tcp --dport 22 -j ACCEPT`</mark> | Delete specific rule  |

### <mark style="color:purple;">Flush Rules</mark>

| Command                                                             | Description                    |
| ------------------------------------------------------------------- | ------------------------------ |
| <mark style="color:yellow;">`iptables -t [table] -F`</mark>         | Flush all rules in \[table]    |
| <mark style="color:yellow;">`iptables -t [table] -F <chain>`</mark> | Flush all rules in in \[table] |

### <mark style="color:purple;">Zero out the Packet and Byte Counters</mark>

| Command                                                             | Description                                                     |
| ------------------------------------------------------------------- | --------------------------------------------------------------- |
| <mark style="color:yellow;">`iptables -t [table] -Z`</mark>         | Zero the packet and byte counters in all chains of the \[table] |
| <mark style="color:yellow;">`iptables -t [table] -Z <chain>`</mark> | Zero the packet and byte counters in of the \[table]            |

### <mark style="color:purple;">Save/Restore iptables</mark>

| Command                                                                               | Description                               |
| ------------------------------------------------------------------------------------- | ----------------------------------------- |
| <mark style="color:yellow;">`iptables-save -t [table] > /[table]_rules_backup`</mark> | Save the current iptables rules to a file |
| <mark style="color:yellow;">`iptables-restore < /[table]_rules_backup`</mark>         | Restore iptables rules from a file        |

### <mark style="color:purple;">Custom Chains</mark>

| Command                                                                       | Description                                         |
| ----------------------------------------------------------------------------- | --------------------------------------------------- |
| <mark style="color:yellow;">`iptables -t [table] -N MYCHAIN`</mark>           | Create custom chain MYCHAIN                         |
| <mark style="color:yellow;">`iptables -t [table] -X MYCHAIN`</mark>           | Delete custom chain MYCHAIN (only if no references) |
| <mark style="color:yellow;">`iptables -t [table] -E OLDCHAIN NEWCHAIN`</mark> | Rename chain from OLDCHAIN to NEWCHAIN              |

### <mark style="color:purple;">RETURN Action</mark>

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
