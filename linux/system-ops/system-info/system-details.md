---
description: Kernel version, uptime, and other information to characterize the system.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# System Details

## <mark style="color:purple;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="261">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>uname -a</code></td><td>Prints kernel name, release, and version.</td></tr><tr><td><mark style="color:yellow;"><code>uname -r</code></td><td>Prints just the kernel release.</td></tr><tr><td><mark style="color:yellow;"><code>uname -v</code></td><td>Prints the kernel version.</td></tr><tr><td><mark style="color:yellow;"><code>uname -o</code></td><td>Prints the operating system.</td></tr><tr><td><mark style="color:yellow;"><code>uname -i</code></td><td>Prints the hardware platform.</td></tr><tr><td><mark style="color:yellow;"><code>cat /etc/*rel*</code></td><td>Prints information regarding the OS.</td></tr><tr><td><mark style="color:yellow;"><code>cat /etc/issue</code></td><td>Displays distribution-specific information.</td></tr><tr><td><mark style="color:yellow;"><code>cat /etc/*-release</code></td><td>Displays distribution information.</td></tr><tr><td><mark style="color:yellow;"><code>cat /etc/os-release</code></td><td>Displays operating system details.</td></tr><tr><td><mark style="color:yellow;"><code>uptime</code></td><td>Displays system uptime.</td></tr><tr><td><mark style="color:yellow;"><code>lsb_release -a</code></td><td>Shows Linux distribution information.</td></tr><tr><td><mark style="color:yellow;"><code>hostnamectl</code></td><td>Displays the system hostname and other system information (systemd systems).</td></tr></tbody></table>

## <mark style="color:purple;">File Locations</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="305">Path</th><th>Description</th></tr></thead><tbody><tr><td>/etc/os-release or /usr/lib/os-release</td><td>On modern Linux distributions adhering to the Freedesktop.org Desktop Entry Specification, contains OS and version information. Provides structured data including operating system name, version, ID, and more.</td></tr><tr><td>/etc/lsb-release</td><td>Stores OS and version information on some distributions like Ubuntu. Contains distribution ID, release number, and description.</td></tr><tr><td>/etc/redhat-release</td><td>Typically found on Red Hat-based distributions such as Red Hat Enterprise Linux (RHEL) and CentOS. Contains distribution name and version.</td></tr><tr><td>/etc/debian_version</td><td>Stores the Debian release version on Debian-based distributions like Debian and Ubuntu.</td></tr><tr><td>/etc/issue or /etc/issue.net</td><td>May contain a message or banner with OS information, typically displayed during system startup or login.</td></tr><tr><td>/proc/version</td><td>Contains information about the kernel version and build date. Often used to determine the kernel version.</td></tr><tr><td>/etc/hostname</td><td>Stores the system hostname on some Unix systems.</td></tr><tr><td>/etc/*-release</td><td>Some distributions may have release-specific files in the /etc/ directory, such as /etc/centos-release or /etc/centos-release-upstream on CentOS.</td></tr><tr><td>ls /etc/<em>release</em></td><td>Lists files related to release information in the /etc/ directory.</td></tr></tbody></table>
