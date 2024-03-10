---
description: Identify the init system in use.
---

# Init System Identification

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="492">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ps -p 1</code></mark></td><td>Checks the PID 1 process. The name can indicate the init system (systemd, init, etc.).</td></tr><tr><td><mark style="color:yellow;"><code>ps -p 1 -o comm=</code></mark></td><td>PID 1 CMD field only.</td></tr><tr><td><mark style="color:yellow;"><code>systemctl</code></mark></td><td>Presence indicates <mark style="color:orange;"><strong>systemd</strong></mark>. If command runs, your system uses <mark style="color:orange;"><strong>systemd</strong></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>systemctl --version</code></mark></td><td>If present, usually indicates <mark style="color:orange;"><strong>systemd</strong></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>stat /proc/1/exe</code></mark></td><td>Displays info about the init process. Follow the symlink to see if it points to <mark style="color:orange;"><strong>systemd</strong></mark>, <mark style="color:orange;"><strong>upstart</strong></mark>, etc.</td></tr><tr><td><mark style="color:yellow;"><code>stat /sbin/init</code></mark></td><td>Symbolic link to <mark style="color:orange;"><strong>Upstart's</strong></mark> process.</td></tr><tr><td><mark style="color:yellow;"><code>/proc/1/comm</code></mark></td><td>Reads the process name of PID 1 directly from the kernel.</td></tr><tr><td><mark style="color:yellow;"><code>ls /sbin/init</code></mark></td><td>Checks what /sbin/init points to. It can be a symlink to the actual init system like <mark style="color:orange;"><strong>systemd</strong></mark> or <mark style="color:orange;"><strong>upstart</strong></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>ls /etc/init.d</code></mark></td><td>Presence of scripts in /etc/init.d often suggests <mark style="color:orange;"><strong>sysvinit</strong></mark> or *Upstart.</td></tr><tr><td><mark style="color:yellow;"><code>ls /etc/init</code></mark></td><td>Presence of upstart config files means it's <mark style="color:orange;"><strong>Upstart</strong></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>initctl</code></mark></td><td>If present, <mark style="color:orange;"><strong>Upstart</strong></mark> is likely.</td></tr><tr><td><mark style="color:yellow;"><code>lsb_release -a</code></mark></td><td>Displays Linux distribution information, sometimes including init system type.</td></tr><tr><td><mark style="color:yellow;"><code>man init</code></mark></td><td>Can reveal Init System.</td></tr></tbody></table>

Checks for a systemd-specific directory:

```bash
test -d /run/systemd/system && echo "systemd"
```

Shows location of systemd files. (/usr/lib/systemd/systemd):

```bash
sudo ls -latr /proc/1/exe
```



Reading CMD Field for PID 1:\
<mark style="color:orange;">**systemd**</mark>: systemd\
<mark style="color:orange;">**sysvinit**</mark>: init\
<mark style="color:orange;">**Upstart**</mark>: /sbin/init (symbolic link to Upstart's process)



## <mark style="color:red;">SysV</mark>

### <mark style="color:purple;">Boot Process</mark>

<mark style="color:orange;">**BIOS**</mark>

<mark style="color:orange;">**MBR**</mark> - Finds and executes GRUB

<mark style="color:orange;">**GRUB**</mark> - Select OS to run, loads kernel

<mark style="color:orange;">**Kernel**</mark> - Once kernel connects to filesystem it moves to init phase

<mark style="color:orange;">**Init**</mark> - kernel reads script /sbin/init.\
This script kicks off services. It looks in /etc/inittab for the initdefault entry (initdefault:3). \
Once it finds this level, it looks for the run scripts which are stored in /etc/rc.d OR /etc.

The scripts look like this:

`/etc/rc.d/rc3.d` OR `/etc/rc3.d`

<mark style="color:orange;">**Run**</mark> - Once these scripts are done, the system is running.



### <mark style="color:purple;">Boot Levels</mark>

0 – Halt

1 – Single User

2 – Multi User (Without NFS or networking features)

3 – Multi User (Typically the default. Can have GUI, but most systems use run level 5 for that.)

4 – User Defined (Basically means if you want to create your own run level you can.)

5 – X11: A graphical protocol that allows you to have a GUI.&#x20;

6 – Reboot



## <mark style="color:red;">Systemd</mark>

### <mark style="color:purple;">Milestones (Runlevels)</mark>&#x20;

<mark style="color:orange;">**poweroff.target**</mark> SysV's Halt - 0

<mark style="color:orange;">**rescue.target**</mark> recovery shell, single user-mode - 1

<mark style="color:orange;">**multiuser.target**</mark> SysV's 2-4. Allows you to turn features off an of without restart

<mark style="color:orange;">**graphical.target**</mark> GUI - 5

<mark style="color:orange;">**reboot.target**</mark> Reboot - 6



<mark style="color:yellow;">`runlevel`</mark> - shows current runlevel.



