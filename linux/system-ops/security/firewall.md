# Firewall

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">iptables</mark>

| <mark style="color:yellow;">`sudo iptables -L`</mark>           | All chains.                                        |
| --------------------------------------------------------------- | -------------------------------------------------- |
| <mark style="color:yellow;">`sudo iptables -L INPUT`</mark>     | INPUT chain.                                       |
| <mark style="color:yellow;">`sudo iptables -L OUTPUT`</mark>    | OUTPUT chain.                                      |
| <mark style="color:yellow;">`sudo iptables -L FORWARD`</mark>   | FORWARD chain.                                     |
| <mark style="color:yellow;">`sudo iptables -L ALL`</mark>       | ALL chains.                                        |
| <mark style="color:yellow;">`sudo iptables -t nat -L`</mark>    | NAT table.                                         |
| <mark style="color:yellow;">`sudo iptables -S`</mark>           | More detailed format.                              |
| <mark style="color:yellow;">`sudo iptables -S INPUT`</mark>     | INPUT chain in a detailed format.                  |
| <mark style="color:yellow;">`sudo iptables -S OUTPUT`</mark>    | OUTPUT chain in a detailed format.                 |
| <mark style="color:yellow;">`sudo iptables -S FORWARD`</mark>   | FORWARD chain in a detailed format.                |
| <mark style="color:yellow;">`sudo iptables -S ALL`</mark>       | ALL chains in a detailed format.                   |
| <mark style="color:yellow;">`sudo iptables -nvL`</mark>         | Include packet and byte counters.                  |
| <mark style="color:yellow;">`sudo iptables -nvL INPUT`</mark>   | INPUT chain along with packet and byte counters.   |
| <mark style="color:yellow;">`sudo iptables -nvL OUTPUT`</mark>  | OUTPUT chain along with packet and byte counters.  |
| <mark style="color:yellow;">`sudo iptables -nvL FORWARD`</mark> | FORWARD chain along with packet and byte counters. |

### <mark style="color:purple;">nftables</mark>

| <mark style="color:yellow;">`nft list ruleset`</mark>                         | Lists all rules in the nftables ruleset.                     |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------ |
| <mark style="color:yellow;">`nft list table <table_name>`</mark>              | Lists all rules within the specified table.                  |
| <mark style="color:yellow;">`nft list chain <table_name> <chain_name>`</mark> | Lists all rules within the specified chain of a table.       |
| <mark style="color:yellow;">`nft list ruleset -a`</mark>                      | Lists all rules in the nftables ruleset, including counters. |
| <mark style="color:yellow;">`nft list ruleset <table_name>`</mark>            | List all rules in specified table.                           |
| <mark style="color:yellow;">`nft list tables`</mark>                          | Lists all tables in the nftables ruleset.                    |
| <mark style="color:yellow;">`nft list table nat`</mark>                       | Lists all rules within the nat table.                        |
| <mark style="color:yellow;">`nft list table filter`</mark>                    | Lists all rules within the filter table.                     |
| <mark style="color:yellow;">`nft list table raw`</mark>                       | Lists all rules within the raw table.                        |

#### <mark style="color:green;">Common Tables:</mark>

<table data-header-hidden><thead><tr><th width="119">Table</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:orange;">inet</mark></td><td>Handles both IPv4 and IPv6 traffic. Often the only one needed for basic firewall configurations.</td></tr><tr><td><mark style="color:orange;">ip</mark></td><td>Specifically handles IPv4 traffic. Useful if only managing IPv4 firewall rules.</td></tr><tr><td><mark style="color:orange;">arp</mark></td><td>Deals with Address Resolution Protocol (ARP) packets. Important for managing ARP-related traffic.</td></tr><tr><td><mark style="color:orange;">bridge</mark></td><td>Handles traffic on bridge devices, commonly used in virtualized environments.</td></tr></tbody></table>

#### <mark style="color:green;">Common Chains:</mark>

<table data-header-hidden><thead><tr><th width="117">Chain</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:orange;">filter</mark></td><td>Responsible for filtering incoming and outgoing traffic based on various criteria.</td></tr><tr><td><mark style="color:orange;">nat</mark></td><td>Performs Network Address Translation (NAT), modifying source or destination addresses of packets.</td></tr><tr><td><mark style="color:orange;">mangle</mark></td><td>Allows manipulating packet header information for advanced traffic shaping or marking.</td></tr></tbody></table>

### <mark style="color:purple;">firewalld</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-zones</code></mark></td><td>Lists all available firewall zones.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-default-zone</code></mark></td><td>Shows the currently active zone.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-active-zones</code></mark></td><td>Displays all currently active zones.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --zone=[zone] --list-all</code></mark></td><td>Lists all rules and settings for a specific zone.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-services</code></mark></td><td>Lists all available firewall services.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --list-services</code></mark></td><td>Lists all services allowed through the firewall.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-service [service_name]</code></mark></td><td>Shows details of a specific service.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --query-service=[service_name]</code></mark></td><td>Checks if a specific service is enabled in the firewall.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-services --permanent</code></mark></td><td>Lists services defined in the permanent configuration.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --list-all</code></mark></td><td>Lists all firewall rules, zones, and services configured.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --list-all --zone [zone_name]</code></mark></td><td>Shows rules in a specific zone.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --list-all --permanent</code></mark></td><td>Lists rules defined in the permanent configuration.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --list-rich-rules</code></mark></td><td>Lists all rich rules configured in firewalld.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-ports</code></mark></td><td>Lists all open ports across all zones.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --list-ports</code></mark></td><td>Lists all ports allowed through the firewall.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-ports --zone [zone_name]</code></mark></td><td>Lists open ports in a specific zone.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-ports --permanent</code></mark></td><td>Lists ports open in the permanent configuration.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-interfaces</code></mark></td><td>Lists all interfaces managed by firewalld.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-interface [interface_name]</code></mark></td><td>Shows details of a specific interface.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --get-interfaces --permanent</code></mark></td><td>Lists interfaces included in the permanent configuration.</td></tr></tbody></table>

## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">firewalld</mark>

#### <mark style="color:green;">Services:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="500">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --add-service [service_name] [--zone [zone_name]]</code></mark></td><td>Adds a service to a specific zone (optional).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --permanent --add-service [service_name]</code></mark></td><td>Adds a service permanently (requires reload).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --remove-service [service_name] [--zone [zone_name]]</code></mark></td><td>Removes a service from a specific zone (optional).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --permanent --remove-service [service_name]</code></mark></td><td>Removes a service permanently (requires reload).</td></tr></tbody></table>

#### <mark style="color:green;">Ports:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="621">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --add-port [port]/[protocol] [--zone [zone_name]]</code></mark></td><td>Opens a port in a specific zone (optional).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --permanent --add-port [port]/[protocol]</code></mark></td><td>Opens a port permanently (requires reload).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --remove-port [port]/[protocol] [--zone [zone_name]]</code></mark></td><td>Closes a port in a specific zone (optional).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --permanent --remove-port [port]/[protocol]</code></mark></td><td>Closes a port permanently (requires reload).</td></tr></tbody></table>

#### <mark style="color:green;">Direct rules:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="612">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --direct --add-rule [rule_string]</code></mark></td><td>Adds a custom rule directly (advanced usage).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --permanent --direct --add-rule [rule_string]</code></mark></td><td>Adds a permanent custom rule (requires reload).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --direct --remove-rule [rule_string]</code></mark></td><td>Removes a custom rule directly (advanced usage).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --permanent --direct --remove-rule [rule_string]</code></mark></td><td>Removes a permanent custom rule (requires reload).</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --add-rich-rule='&#x3C;rule>' --permanent</code></mark></td><td>Adds a rich rule to the firewall permanently.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --remove-rich-rule='&#x3C;rule>' --permanent</code></mark></td><td>Removes a rich rule from the firewall permanently.</td></tr></tbody></table>

#### <mark style="color:green;">Changing the default zone:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="520">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --set-default-zone [zone_name]</code></mark></td><td>Changes the currently active zone.</td></tr></tbody></table>

#### <mark style="color:green;">Reloading the configuration:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="414">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --reload</code></mark></td><td>Applies changes made with --permanent options.</td></tr><tr><td><mark style="color:yellow;"><code>sudo firewall-cmd --complete-reload</code></mark></td><td>Reloads the firewall configuration and resets runtime changes.</td></tr></tbody></table>
