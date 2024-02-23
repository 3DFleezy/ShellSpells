# Hostname / Host ID

## Commands

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>cat /proc/sys/kernel/hostname</code></td><td>Hostname directly from the kernel's hostname file.</td></tr><tr><td><mark style="color:yellow;"><code>hostname</code></td><td>Displays the hostname.</td></tr><tr><td><mark style="color:yellow;"><code>uname -n</code></td><td>Displays just the hostname.</td></tr><tr><td><mark style="color:yellow;"><code>hostnamectl</code></td><td>*systemd systems - Most comprehensive hostname info</td></tr><tr><td><mark style="color:yellow;"><code>cat /etc/hostname</code></td><td>Displays the hostname stored in the /etc/hostname file.</td></tr><tr><td><mark style="color:yellow;"><code>hostid</code></td><td>Prints the numeric identifier for the current host.</td></tr></tbody></table>



Multiple hostnames: A system can have different hostnames configured for various purposes.



### Static vs. transient

<mark style="color:yellow;">`hostnamectl`</mark> distinguishes between static (set in configuration files) and transient (set at runtime) hostnames.



## File Locations

<table data-header-hidden data-full-width="true"><thead><tr><th width="326">Path</th><th>Description</th></tr></thead><tbody><tr><td>/etc/hostname</td><td>On many Linux distributions such as Debian and Ubuntu, stores the system's hostname.</td></tr><tr><td>/etc/hosts</td><td>Contains mappings of IP addresses to hostnames, often includes the system's hostname for the loopback interface.</td></tr><tr><td>/etc/sysconfig/network</td><td>On Red Hat-based distributions like Red Hat Enterprise Linux (RHEL) and CentOS, sets the system's hostname.</td></tr><tr><td>/etc/rc.conf or /etc/rc.conf.local</td><td>On some Unix systems like FreeBSD, stores the hostname information.</td></tr><tr><td>Dynamic Host Configuration Protocol</td><td>In network configurations using DHCP, the hostname may be assigned dynamically by the DHCP server.</td></tr><tr><td>hostname command</td><td>Used to view or change the hostname temporarily during a session.</td></tr><tr><td>Network Configuration Files</td><td>Some Unix distributions store hostname information in network configuration files.</td></tr><tr><td>NIS/NIS+</td><td>In network environments using NIS or NIS+ for centralized authentication and configuration management.</td></tr></tbody></table>

