# Packages

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Debian-based Systems</mark>&#x20;

e.g., Debian, Ubuntu

<table data-header-hidden data-full-width="true"><thead><tr><th width="280">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>dpkg -l</code></td><td>Lists all installed packages using the Debian package manager.</td></tr><tr><td><code>apt list --installed</code></td><td>Lists all installed packages using the Advanced Package Tool (APT).</td></tr><tr><td><code>aptitude search '~i'</code></td><td>Lists all installed packages using the Aptitude package manager.</td></tr></tbody></table>



### <mark style="color:purple;">Red Hat-based Systems</mark>&#x20;

e.g., Red Hat Enterprise Linux, CentOS

<table data-header-hidden data-full-width="true"><thead><tr><th width="275">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>rpm -qa</code></td><td>Lists all installed packages using the RPM Package Manager.</td></tr><tr><td><code>yum list installed</code></td><td>Lists all installed packages using the Yellowdog Updater, Modified (YUM) package manager.</td></tr></tbody></table>



### <mark style="color:purple;">Systems with DNF Package Manager</mark>&#x20;

e.g., Fedora, CentOS 8+

<table data-header-hidden data-full-width="true"><thead><tr><th width="273">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>dnf list installed</code></td><td>Lists all installed packages using the DNF package manager.package manager.</td></tr></tbody></table>



### <mark style="color:purple;">Systems with Pacman Package Manager</mark>&#x20;

e.g., Arch Linux

<table data-header-hidden data-full-width="true"><thead><tr><th width="272">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>pacman -Q</code></td><td>Lists all installed packages using the Pacman package manager.</td></tr></tbody></table>



### <mark style="color:purple;">Systems with the Zypper Package Manager</mark>&#x20;

e.g., openSUSE

<table data-header-hidden data-full-width="true"><thead><tr><th width="310">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>zypper se --installed-only</code></td><td>Lists all installed packages using the Zypper package manager.</td></tr></tbody></table>





## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">Debian-based Systems</mark>

e.g., Debian, Ubuntu

<table data-header-hidden data-full-width="true"><thead><tr><th width="408">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>apt install package_name</code></td><td>Installs a package using the Advanced Package Tool (APT).</td></tr><tr><td><code>apt update &#x26;&#x26; apt upgrade</code></td><td>Updates the package list and upgrades installed packages.</td></tr></tbody></table>



### <mark style="color:purple;">Red Hat-based Systems</mark>

e.g., Red Hat Enterprise Linux, CentOS

<table data-header-hidden data-full-width="true"><thead><tr><th width="405">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>yum install package_name</code></td><td>Installs a package using the Yellowdog Updater, Modified (YUM) package manager.</td></tr><tr><td><code>yum update</code></td><td>Updates all installed packages using YUM.</td></tr></tbody></table>



### <mark style="color:purple;">Systems withDNF Package Manager</mark>

e.g., Fedora, CentOS 8+

<table data-header-hidden data-full-width="true"><thead><tr><th width="407">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>dnf install package_name</code></td><td>Installs a package using the DNF package manager.</td></tr><tr><td><code>dnf update</code></td><td>Updates all installed packages using DNF.</td></tr></tbody></table>



### <mark style="color:purple;">Systems withPacman Package Manager</mark>&#x20;

e.g., Arch Linux

<table data-header-hidden data-full-width="true"><thead><tr><th width="400">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>pacman -S package_name</code></td><td>Installs a package using the Pacman package manager.</td></tr><tr><td><code>pacman -Syu</code></td><td>Synchronizes package databases and upgrades installed packages.</td></tr></tbody></table>



### <mark style="color:purple;">Systems with Zypper Package Manager</mark>&#x20;

e.g., openSUSE

<table data-header-hidden data-full-width="true"><thead><tr><th width="400">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>zypper install package_name</code></td><td>Installs a package using the Zypper package manager.</td></tr><tr><td><code>zypper update</code></td><td>Updates all installed packages using Zypper.</td></tr></tbody></table>



### <mark style="color:purple;">Manual install</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="401">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>./configure &#x26;&#x26; make &#x26;&#x26; make install</code></td><td>Manual installation from source code.</td></tr></tbody></table>
