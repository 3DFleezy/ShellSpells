# Firewall

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">iptables</mark>

| Command                      | Description                                        |
| ---------------------------- | -------------------------------------------------- |
| `sudo iptables -L`           | All chains.                                        |
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

| Command                                    | Description                                                  |
| ------------------------------------------ | ------------------------------------------------------------ |
| `nft list ruleset`                         | Lists all rules in the nftables ruleset.                     |
| `nft list table <table_name>`              | Lists all rules within the specified table.                  |
| `nft list chain <table_name> <chain_name>` | Lists all rules within the specified chain of a table.       |
| `nft list ruleset -a`                      | Lists all rules in the nftables ruleset, including counters. |
| `nft list ruleset <table_name>`            | List all rules in specified table.                           |
| `nft list tables`                          | Lists all tables in the nftables ruleset.                    |
| `nft list table nat`                       | Lists all rules within the nat table.                        |
| `nft list table filter`                    | Lists all rules within the filter table.                     |
| `nft list table raw`                       | Lists all rules within the raw table.                        |

#### <mark style="color:green;">Common Tables:</mark>

| Table    | Description                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------- |
| \*inet   | Handles both IPv4 and IPv6 traffic. Often the only one needed for basic firewall configurations.  |
| \*ip     | Specifically handles IPv4 traffic. Useful if only managing IPv4 firewall rules.                   |
| \*arp    | Deals with Address Resolution Protocol (ARP) packets. Important for managing ARP-related traffic. |
| \*bridge | Handles traffic on bridge devices, commonly used in virtualized environments.                     |

#### <mark style="color:green;">Common Chains:</mark>

| Chain    | Description                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------- |
| \*filter | Responsible for filtering incoming and outgoing traffic based on various criteria.                |
| \*nat    | Performs Network Address Translation (NAT), modifying source or destination addresses of packets. |
| \*mangle | Allows manipulating packet header information for advanced traffic shaping or marking.            |



### <mark style="color:purple;">firewalld</mark>

| Command                                              | Description                                               |
| ---------------------------------------------------- | --------------------------------------------------------- |
| `sudo firewall-cmd --get-zones`                      | Lists all available firewall zones.                       |
| `sudo firewall-cmd --get-default-zone`               | Shows the currently active zone.                          |
| `sudo firewall-cmd --get-active-zones`               | Displays all currently active zones.                      |
| `sudo firewall-cmd --zone=[zone] --list-all`         | Lists all rules and settings for a specific zone.         |
| `sudo firewall-cmd --get-services`                   | Lists all available firewall services.                    |
| `sudo firewall-cmd --list-services`                  | Lists all services allowed through the firewall.          |
| `sudo firewall-cmd --get-service [service_name]`     | Shows details of a specific service.                      |
| `sudo firewall-cmd --query-service=[service_name]`   | Checks if a specific service is enabled in the firewall.  |
| `sudo firewall-cmd --get-services --permanent`       | Lists services defined in the permanent configuration.    |
| `sudo firewall-cmd --list-all`                       | Lists all firewall rules, zones, and services configured. |
| `sudo firewall-cmd --list-all --zone [zone_name]`    | Shows rules in a specific zone.                           |
| `sudo firewall-cmd --list-all --permanent`           | Lists rules defined in the permanent configuration.       |
| `sudo firewall-cmd --list-rich-rules`                | Lists all rich rules configured in firewalld.             |
| `sudo firewall-cmd --get-ports`                      | Lists all open ports across all zones.                    |
| `sudo firewall-cmd --list-ports`                     | Lists all ports allowed through the firewall.             |
| `sudo firewall-cmd --get-ports --zone [zone_name]`   | Lists open ports in a specific zone.                      |
| `sudo firewall-cmd --get-ports --permanent`          | Lists ports open in the permanent configuration.          |
| `sudo firewall-cmd --get-interfaces`                 | Lists all interfaces managed by firewalld.                |
| `sudo firewall-cmd --get-interface [interface_name]` | Shows details of a specific interface.                    |
| `sudo firewall-cmd --get-interfaces --permanent`     | Lists interfaces included in the permanent configuration. |



## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">firewalld</mark>

#### <mark style="color:green;">Services:</mark>

| Command                                                                  | Description                                        |
| ------------------------------------------------------------------------ | -------------------------------------------------- |
| `sudo firewall-cmd --add-service [service_name] [--zone [zone_name]]`    | Adds a service to a specific zone (optional).      |
| `sudo firewall-cmd --permanent --add-service [service_name]`             | Adds a service permanently (requires reload).      |
| `sudo firewall-cmd --remove-service [service_name] [--zone [zone_name]]` | Removes a service from a specific zone (optional). |
| `sudo firewall-cmd --permanent --remove-service [service_name]`          | Removes a service permanently (requires reload).   |

#### <mark style="color:green;">Ports:</mark>

| Command                                                                  | Description                                  |
| ------------------------------------------------------------------------ | -------------------------------------------- |
| `sudo firewall-cmd --add-port [port]/[protocol] [--zone [zone_name]]`    | Opens a port in a specific zone (optional).  |
| `sudo firewall-cmd --permanent --add-port [port]/[protocol]`             | Opens a port permanently (requires reload).  |
| `sudo firewall-cmd --remove-port [port]/[protocol] [--zone [zone_name]]` | Closes a port in a specific zone (optional). |
| `sudo firewall-cmd --permanent --remove-port [port]/[protocol]`          | Closes a port permanently (requires reload). |

#### <mark style="color:green;">Direct rules:</mark>

| Command                                                              | Description                                        |
| -------------------------------------------------------------------- | -------------------------------------------------- |
| `sudo firewall-cmd --direct --add-rule [rule_string]`                | Adds a custom rule directly (advanced usage).      |
| `sudo firewall-cmd --permanent --direct --add-rule [rule_string]`    | Adds a permanent custom rule (requires reload).    |
| `sudo firewall-cmd --direct --remove-rule [rule_string]`             | Removes a custom rule directly (advanced usage).   |
| `sudo firewall-cmd --permanent --direct --remove-rule [rule_string]` | Removes a permanent custom rule (requires reload). |
| `sudo firewall-cmd --add-rich-rule='<rule>' --permanent`             | Adds a rich rule to the firewall permanently.      |
| `sudo firewall-cmd --remove-rich-rule='<rule>' --permanent`          | Removes a rich rule from the firewall permanently. |

#### <mark style="color:green;">Changing the default zone:</mark>

| Command                                            | Description                        |
| -------------------------------------------------- | ---------------------------------- |
| `sudo firewall-cmd --set-default-zone [zone_name]` | Changes the currently active zone. |

#### <mark style="color:green;">Reloading the configuration:</mark>

| Command                               | Description                                                    |
| ------------------------------------- | -------------------------------------------------------------- |
| `sudo firewall-cmd --reload`          | Applies changes made with --permanent options.                 |
| `sudo firewall-cmd --complete-reload` | Reloads the firewall configuration and resets runtime changes. |
