# Packages

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Debian-based Systems</mark>&#x20;

e.g., Debian, Ubuntu

<table data-header-hidden data-full-width="false"><thead><tr><th width="280">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>dpkg -l</code></td><td>Lists all installed packages using the Debian package manager.</td></tr><tr><td><code>apt list --installed</code></td><td>Lists all installed packages using the Advanced Package Tool (APT).</td></tr><tr><td><code>aptitude search '~i'</code></td><td>Lists all installed packages using the Aptitude package manager.</td></tr></tbody></table>



### <mark style="color:purple;">Red Hat-based Systems</mark>&#x20;

e.g., Red Hat Enterprise Linux, CentOS

<table data-header-hidden data-full-width="false"><thead><tr><th width="275">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>rpm -qa</code></td><td>Lists all installed packages using the RPM Package Manager.</td></tr><tr><td><code>yum list installed</code></td><td>Lists all installed packages using the Yellowdog Updater, Modified (YUM) package manager.</td></tr></tbody></table>



### <mark style="color:purple;">Systems with DNF Package Manager</mark>&#x20;

e.g., Fedora, CentOS 8+

<table data-header-hidden data-full-width="false"><thead><tr><th width="273">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>dnf list installed</code></td><td>Lists all installed packages using the DNF package manager.package manager.</td></tr></tbody></table>



### <mark style="color:purple;">Systems with Pacman Package Manager</mark>&#x20;

e.g., Arch Linux

<table data-header-hidden data-full-width="false"><thead><tr><th width="272">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>pacman -Q</code></td><td>Lists all installed packages using the Pacman package manager.</td></tr></tbody></table>



### <mark style="color:purple;">Systems with the Zypper Package Manager</mark>&#x20;

e.g., openSUSE

<table data-header-hidden data-full-width="false"><thead><tr><th width="310">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>zypper se --installed-only</code></td><td>Lists all installed packages using the Zypper package manager.</td></tr></tbody></table>





## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">Debian-based Systems</mark>

e.g., Debian, Ubuntu

<table data-header-hidden data-full-width="false"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>apt install package_name</code></td><td>Installs a package using the Advanced Package Tool (APT).</td></tr><tr><td><code>apt update &#x26;&#x26; apt upgrade</code></td><td>Updates the package list and upgrades installed packages.</td></tr></tbody></table>



### <mark style="color:purple;">Red Hat-based Systems</mark>

e.g., Red Hat Enterprise Linux, CentOS

| `yum install package_name` | Installs a package using the Yellowdog Updater, Modified (YUM) package manager. |
| -------------------------- | ------------------------------------------------------------------------------- |
| `yum update`               | Updates all installed packages using YUM.                                       |



### <mark style="color:purple;">Systems withDNF Package Manager</mark>

e.g., Fedora, CentOS 8+

| `dnf install package_name` | Installs a package using the DNF package manager. |
| -------------------------- | ------------------------------------------------- |
| `dnf update`               | Updates all installed packages using DNF.         |



### <mark style="color:purple;">Systems withPacman Package Manager</mark>&#x20;

e.g., Arch Linux

| `pacman -S package_name` | Installs a package using the Pacman package manager.            |
| ------------------------ | --------------------------------------------------------------- |
| `pacman -Syu`            | Synchronizes package databases and upgrades installed packages. |



### <mark style="color:purple;">Systems with Zypper Package Manager</mark>&#x20;

e.g., openSUSE

| `zypper install package_name` | Installs a package using the Zypper package manager. |
| ----------------------------- | ---------------------------------------------------- |
| `zypper update`               | Updates all installed packages using Zypper.         |



### <mark style="color:purple;">Manual install</mark>

| `./configure && make && make install` | Manual installation from source code. |
| ------------------------------------- | ------------------------------------- |
