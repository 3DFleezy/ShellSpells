# Firewall

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">iptables</mark>

| `sudo iptables -L`           | All chains.                                        |
| ---------------------------- | -------------------------------------------------- |
| `sudo iptables -L INPUT`     | INPUT chain.                                       |
| `sudo iptables -L OUTPUT`    | OUTPUT chain.                                      |
| `sudo iptables -L FORWARD`   | FORWARD chain.                                     |
| `sudo iptables -L ALL`       | ALL chains.                                        |
| `sudo iptables -t nat -L`    | NAT table.                                         |
| `sudo iptables -S`           | More detailed format.                              |
| `sudo iptables -S INPUT`     | INPUT chain in a detailed format.                  |
| `sudo iptables -S OUTPUT`    | OUTPUT chain in a detailed format.                 |
| `sudo iptables -S FORWARD`   | FORWARD chain in a detailed format.                |
| `sudo iptables -S ALL`       | ALL chains in a detailed format.                   |
| `sudo iptables -nvL`         | Include packet and byte counters.                  |
| `sudo iptables -nvL INPUT`   | INPUT chain along with packet and byte counters.   |
| `sudo iptables -nvL OUTPUT`  | OUTPUT chain along with packet and byte counters.  |
| `sudo iptables -nvL FORWARD` | FORWARD chain along with packet and byte counters. |



### <mark style="color:purple;">nftables</mark>

| `nft list ruleset`                         | Lists all rules in the nftables ruleset.                     |
| ------------------------------------------ | ------------------------------------------------------------ |
| `nft list table <table_name>`              | Lists all rules within the specified table.                  |
| `nft list chain <table_name> <chain_name>` | Lists all rules within the specified chain of a table.       |
| `nft list ruleset -a`                      | Lists all rules in the nftables ruleset, including counters. |
| `nft list ruleset <table_name>`            | List all rules in specified table.                           |
| `nft list tables`                          | Lists all tables in the nftables ruleset.                    |
| `nft list table nat`                       | Lists all rules within the nat table.                        |
| `nft list table filter`                    | Lists all rules within the filter table.                     |
| `nft list table raw`                       | Lists all rules within the raw table.                        |

#### <mark style="color:green;">Common Tables:</mark>

<table data-header-hidden><thead><tr><th width="119">Table</th><th>Description</th></tr></thead><tbody><tr><td>*inet</td><td>Handles both IPv4 and IPv6 traffic. Often the only one needed for basic firewall configurations.</td></tr><tr><td>*ip</td><td>Specifically handles IPv4 traffic. Useful if only managing IPv4 firewall rules.</td></tr><tr><td>*arp</td><td>Deals with Address Resolution Protocol (ARP) packets. Important for managing ARP-related traffic.</td></tr><tr><td>*bridge</td><td>Handles traffic on bridge devices, commonly used in virtualized environments.</td></tr></tbody></table>

#### <mark style="color:green;">Common Chains:</mark>

<table data-header-hidden><thead><tr><th width="117">Chain</th><th>Description</th></tr></thead><tbody><tr><td>*filter</td><td>Responsible for filtering incoming and outgoing traffic based on various criteria.</td></tr><tr><td>*nat</td><td>Performs Network Address Translation (NAT), modifying source or destination addresses of packets.</td></tr><tr><td>*mangle</td><td>Allows manipulating packet header information for advanced traffic shaping or marking.</td></tr></tbody></table>



### <mark style="color:purple;">firewalld</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sudo firewall-cmd --get-zones</code></td><td>Lists all available firewall zones.</td></tr><tr><td><code>sudo firewall-cmd --get-default-zone</code></td><td>Shows the currently active zone.</td></tr><tr><td><code>sudo firewall-cmd --get-active-zones</code></td><td>Displays all currently active zones.</td></tr><tr><td><code>sudo firewall-cmd --zone=[zone] --list-all</code></td><td>Lists all rules and settings for a specific zone.</td></tr><tr><td><code>sudo firewall-cmd --get-services</code></td><td>Lists all available firewall services.</td></tr><tr><td><code>sudo firewall-cmd --list-services</code></td><td>Lists all services allowed through the firewall.</td></tr><tr><td><code>sudo firewall-cmd --get-service [service_name]</code></td><td>Shows details of a specific service.</td></tr><tr><td><code>sudo firewall-cmd --query-service=[service_name]</code></td><td>Checks if a specific service is enabled in the firewall.</td></tr><tr><td><code>sudo firewall-cmd --get-services --permanent</code></td><td>Lists services defined in the permanent configuration.</td></tr><tr><td><code>sudo firewall-cmd --list-all</code></td><td>Lists all firewall rules, zones, and services configured.</td></tr><tr><td><code>sudo firewall-cmd --list-all --zone [zone_name]</code></td><td>Shows rules in a specific zone.</td></tr><tr><td><code>sudo firewall-cmd --list-all --permanent</code></td><td>Lists rules defined in the permanent configuration.</td></tr><tr><td><code>sudo firewall-cmd --list-rich-rules</code></td><td>Lists all rich rules configured in firewalld.</td></tr><tr><td><code>sudo firewall-cmd --get-ports</code></td><td>Lists all open ports across all zones.</td></tr><tr><td><code>sudo firewall-cmd --list-ports</code></td><td>Lists all ports allowed through the firewall.</td></tr><tr><td><code>sudo firewall-cmd --get-ports --zone [zone_name]</code></td><td>Lists open ports in a specific zone.</td></tr><tr><td><code>sudo firewall-cmd --get-ports --permanent</code></td><td>Lists ports open in the permanent configuration.</td></tr><tr><td><code>sudo firewall-cmd --get-interfaces</code></td><td>Lists all interfaces managed by firewalld.</td></tr><tr><td><code>sudo firewall-cmd --get-interface [interface_name]</code></td><td>Shows details of a specific interface.</td></tr><tr><td><code>sudo firewall-cmd --get-interfaces --permanent</code></td><td>Lists interfaces included in the permanent configuration.</td></tr></tbody></table>



## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">firewalld</mark>

#### <mark style="color:green;">Services:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="500">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sudo firewall-cmd --add-service [service_name] [--zone [zone_name]]</code></td><td>Adds a service to a specific zone (optional).</td></tr><tr><td><code>sudo firewall-cmd --permanent --add-service [service_name]</code></td><td>Adds a service permanently (requires reload).</td></tr><tr><td><code>sudo firewall-cmd --remove-service [service_name] [--zone [zone_name]]</code></td><td>Removes a service from a specific zone (optional).</td></tr><tr><td><code>sudo firewall-cmd --permanent --remove-service [service_name]</code></td><td>Removes a service permanently (requires reload).</td></tr></tbody></table>

#### <mark style="color:green;">Ports:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="621">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sudo firewall-cmd --add-port [port]/[protocol] [--zone [zone_name]]</code></td><td>Opens a port in a specific zone (optional).</td></tr><tr><td><code>sudo firewall-cmd --permanent --add-port [port]/[protocol]</code></td><td>Opens a port permanently (requires reload).</td></tr><tr><td><code>sudo firewall-cmd --remove-port [port]/[protocol] [--zone [zone_name]]</code></td><td>Closes a port in a specific zone (optional).</td></tr><tr><td><code>sudo firewall-cmd --permanent --remove-port [port]/[protocol]</code></td><td>Closes a port permanently (requires reload).</td></tr></tbody></table>

#### <mark style="color:green;">Direct rules:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="612">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sudo firewall-cmd --direct --add-rule [rule_string]</code></td><td>Adds a custom rule directly (advanced usage).</td></tr><tr><td><code>sudo firewall-cmd --permanent --direct --add-rule [rule_string]</code></td><td>Adds a permanent custom rule (requires reload).</td></tr><tr><td><code>sudo firewall-cmd --direct --remove-rule [rule_string]</code></td><td>Removes a custom rule directly (advanced usage).</td></tr><tr><td><code>sudo firewall-cmd --permanent --direct --remove-rule [rule_string]</code></td><td>Removes a permanent custom rule (requires reload).</td></tr><tr><td><code>sudo firewall-cmd --add-rich-rule='&#x3C;rule>' --permanent</code></td><td>Adds a rich rule to the firewall permanently.</td></tr><tr><td><code>sudo firewall-cmd --remove-rich-rule='&#x3C;rule>' --permanent</code></td><td>Removes a rich rule from the firewall permanently.</td></tr></tbody></table>

#### <mark style="color:green;">Changing the default zone:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="520">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sudo firewall-cmd --set-default-zone [zone_name]</code></td><td>Changes the currently active zone.</td></tr></tbody></table>

#### <mark style="color:green;">Reloading the configuration:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="414">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sudo firewall-cmd --reload</code></td><td>Applies changes made with --permanent options.</td></tr><tr><td><code>sudo firewall-cmd --complete-reload</code></td><td>Reloads the firewall configuration and resets runtime changes.</td></tr></tbody></table>
