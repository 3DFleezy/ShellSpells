---
description: Identify the init system in use.
---

# Init System Identification

<table data-header-hidden data-full-width="true"><thead><tr><th width="492">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>ps -p 1</code></td><td>Checks the PID 1 process. The name can indicate the init system (systemd, init, etc.).</td></tr><tr><td><code>ps -p 1 -o comm=</code></td><td>PID 1 CMD field only.</td></tr><tr><td><code>systemctl</code></td><td>Presence indicates <mark style="color:orange;"><strong>systemd</strong></mark>. If command runs, your system uses <mark style="color:orange;"><strong>systemd</strong></mark>.</td></tr><tr><td><code>systemctl --version</code></td><td>If present, usually indicates <mark style="color:orange;"><strong>systemd</strong></mark>.</td></tr><tr><td><code>stat /proc/1/exe</code></td><td>Displays info about the init process. Follow the symlink to see if it points to <mark style="color:orange;"><strong>systemd</strong></mark>, <mark style="color:orange;"><strong>upstart</strong></mark>, etc.</td></tr><tr><td><code>stat /sbin/init</code></td><td>Symbolic link to <mark style="color:orange;"><strong>Upstart's</strong></mark> process.</td></tr><tr><td><code>/proc/1/comm</code></td><td>Reads the process name of PID 1 directly from the kernel.</td></tr><tr><td><code>ls /sbin/init</code></td><td>Checks what /sbin/init points to. It can be a symlink to the actual init system like <mark style="color:orange;"><strong>systemd</strong></mark> or <mark style="color:orange;"><strong>upstart</strong></mark>.</td></tr><tr><td><code>ls /etc/init.d</code></td><td>Presence of scripts in /etc/init.d often suggests <mark style="color:orange;"><strong>sysvinit</strong></mark> or *Upstart.</td></tr><tr><td><code>ls /etc/init</code></td><td>Presence of upstart config files means it's <mark style="color:orange;"><strong>Upstart</strong></mark>.</td></tr><tr><td><code>initctl</code></td><td>If present, <mark style="color:orange;"><strong>Upstart</strong></mark> is likely.</td></tr><tr><td><code>lsb_release -a</code></td><td>Displays Linux distribution information, sometimes including init system type.</td></tr><tr><td><code>test -d /run/systemd/system &#x26;&#x26; echo "systemd"</code></td><td>Checks for a systemd-specific directory</td></tr></tbody></table>



Reading CMD Field for PID 1:\
<mark style="color:orange;">**systemd**</mark>: systemd \
<mark style="color:orange;">**sysvinit**</mark>: init \
<mark style="color:orange;">**Upstart**</mark>: /sbin/init (symbolic link to Upstart's process)
