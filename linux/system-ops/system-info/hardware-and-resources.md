# Hardware & Resources

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="259">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>inxi</code></td><td>(Not on all systems) Comprehensive hardware and system information.</td></tr><tr><td><mark style="color:yellow;"><code>lshw</code></td><td>Hardware details</td></tr><tr><td><mark style="color:yellow;"><code>uname -m</code></td><td>Machine architecture</td></tr><tr><td><mark style="color:yellow;"><code>uname -v</code></td><td>Kernel version</td></tr><tr><td><mark style="color:yellow;"><code>uname -o</code></td><td>OS</td></tr><tr><td><mark style="color:yellow;"><code>uname -i</code></td><td>Hardware platform</td></tr><tr><td><mark style="color:yellow;"><code>lscpu</code></td><td>CPU</td></tr><tr><td><mark style="color:yellow;"><code>cat /proc/cpuinfo</code></td><td>CPU</td></tr><tr><td><mark style="color:yellow;"><code>uname -p</code></td><td>Processor type</td></tr><tr><td><mark style="color:yellow;"><code>cat /proc/meminfo</code></td><td>Memory</td></tr><tr><td><mark style="color:yellow;"><code>free -m</code></td><td>Displays free and used memory in megabytes.</td></tr><tr><td><mark style="color:yellow;"><code>vmstat</code></td><td>Virtual memory</td></tr><tr><td><mark style="color:yellow;"><code>df -h</code></td><td>Disk space usage</td></tr><tr><td><mark style="color:yellow;"><code>df -h</code></td><td>Disk space usage in human-readable format.</td></tr><tr><td><mark style="color:yellow;"><code>ncdu</code></td><td>Disk usage analyzer</td></tr><tr><td><mark style="color:yellow;"><code>lsblk</code></td><td>List block devices</td></tr><tr><td><mark style="color:yellow;"><code>dmidecode</code></td><td>Info from SMBIOS/DMI tables (motherboard, BIOS, memory, etc.) (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>fdisk -l</code></td><td>Lists disk partitions (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>lspci</code></td><td>Lists all PCI devices.</td></tr><tr><td><mark style="color:yellow;"><code>lsusb</code></td><td>Displays USB devices.</td></tr><tr><td><mark style="color:yellow;"><code>ip addr</code></td><td>Shows network interface information and IP addresses.</td></tr><tr><td><mark style="color:yellow;"><code>du</code></td><td>Estimate file and directory space usage.</td></tr></tbody></table>

### <mark style="color:purple;">Solaris</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="259">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>psrinfo -v</code></td><td>Displays processor information.</td></tr><tr><td><mark style="color:yellow;"><code>modinfo -c</code></td><td>Lists all the kernel modules.</td></tr></tbody></table>



## <mark style="color:red;">File Locations</mark>

Note: `/proc` and `/sys` provide real-time data direct from the kernel and can't be modified by a user. Access to certain files within these directories may require sudo privileges.



### <mark style="color:purple;">/proc</mark>

<table data-header-hidden><thead><tr><th width="225">Path</th><th>Description</th></tr></thead><tbody><tr><td>/proc/cpuinfo</td><td>Information about CPUs.</td></tr><tr><td>/proc/meminfo</td><td>Memory-related information.</td></tr><tr><td>/proc/loadavg</td><td>Load average statistics.</td></tr><tr><td>/proc/uptime</td><td>System uptime.</td></tr><tr><td>/proc/version</td><td>Kernel version.</td></tr><tr><td>/proc/net/</td><td>Network-related information.</td></tr><tr><td>/proc/mounts</td><td>Mounted filesystems.</td></tr><tr><td>/proc/devices</td><td>Available devices.</td></tr><tr><td>/proc/modules</td><td>Loaded kernel modules.</td></tr><tr><td>/proc/interrupts</td><td>IRQ usage.</td></tr></tbody></table>



### <mark style="color:purple;">/sys</mark>

<table data-header-hidden><thead><tr><th width="228">Path</th><th>Description</th></tr></thead><tbody><tr><td>/sys/class/hwmon/</td><td>Hardware monitoring sensors.</td></tr><tr><td>/sys/block/</td><td>Block devices (e.g., hard drives).</td></tr><tr><td>/sys/class/net/</td><td>Network interfaces.</td></tr></tbody></table>



### <mark style="color:purple;">/dev</mark>

Contains device files representing hardware devices on the system. \
While these files can be read from and written to, their contents are managed directly by the kernel and cannot be arbitrarily modified by users.



### <mark style="color:purple;">dmesg</mark>

The kernel message buffer, viewable using the dmesg command, contains logs of system events and hardware messages. \
It's a read-only view of kernel activity and cannot be edited directly.
