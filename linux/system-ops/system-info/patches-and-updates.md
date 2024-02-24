# Patches & Updates

## <mark style="color:red;">Package Management System</mark>

### <mark style="color:purple;">Debian/Ubuntu</mark>

<table data-full-width="true"><thead><tr><th width="386">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>apt list --installed | grep "linux-image"</code></mark></td><td>Lists installed kernel packages, including hotfixes</td></tr><tr><td><mark style="color:yellow;"><code>apt list --upgradable | grep "security"</code></mark></td><td>Filters the list to show only security-related updates.</td></tr><tr><td><mark style="color:yellow;"><code>apt list --upgradable</code></mark></td><td>Lists available updates for all packages, including security patches, on Debian/Ubuntu systems.</td></tr><tr><td><mark style="color:yellow;"><code>apt-get changelog &#x3C;package_name></code></mark></td><td>View detailed changelog for a specific package on Debian/Ubuntu systems.</td></tr></tbody></table>

### <mark style="color:purple;">Red Hat/CentOS</mark>

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>rpm -qa | grep kernel</code></mark></td><td>Lists installed kernel packages</td></tr><tr><td><mark style="color:yellow;"><code>yum check-update</code></mark></td><td>Checks for available updates, including security patches, on Red Hat/CentOS systems.</td></tr><tr><td><mark style="color:yellow;"><code>yum updateinfo list security</code></mark></td><td>Lists available security updates on Red Hat/CentOS systems.</td></tr><tr><td><mark style="color:yellow;"><code>yum updateinfo list updates | grep security</code></mark></td><td>Filters available updates for security-related updates.</td></tr></tbody></table>

### <mark style="color:purple;">SUSE</mark>

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>zypper list-patches</code></mark></td><td>Lists installed patches on SUSE systems.</td></tr><tr><td><mark style="color:yellow;"><code>zypper patch-info &#x3C;patch_number></code></mark></td><td>View details about a specific patch on SUSE systems.</td></tr><tr><td><mark style="color:yellow;"><code>zypper patches --category security</code></mark></td><td>Lists only security-related patches on SUSE systems.</td></tr></tbody></table>

## <mark style="color:purple;">Kernel Version Check</mark>

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>uname -r</code></mark></td><td>Displays the current kernel version.</td></tr></tbody></table>

Compare this version with official release notes or online resources to identify applied hotfixes.

Some distributions might include hotfix information in the kernel release string itself.

## <mark style="color:red;">System Logs</mark>

Search for hotfix-related messages:

```bash
grep -i hotfix /var/log/dmesg
```

```bash
grep -i hotfix /var/log/messages
```

Search package manager logs:

```bash
grep -i hotfix /var/log/apt/history.log
```

```bash
grep -i hotfix /var/log/yum.log
```

Note: Not all hotfixes might be explicitly logged.

## <mark style="color:red;">Specific Tools</mark>

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ksplice</code></mark></td><td>(Oracle Linux): Manages live kernel patching without reboots.</td></tr></tbody></table>

Third-party tools (e.g., `yum-plugin-security`, `zypper-patch-viewer`) might provide additional hotfix-related functionality.
