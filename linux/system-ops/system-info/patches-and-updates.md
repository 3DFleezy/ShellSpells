# Patches & Updates

## <mark style="color:red;">Package Management System</mark>

### <mark style="color:purple;">Debian/Ubuntu</mark>

<table data-full-width="true"><thead><tr><th width="386">Command</th><th>Description</th></tr></thead><tbody><tr><td>`apt list --installed</td><td>grep "linux-image"`</td></tr><tr><td>`apt list --upgradable</td><td>grep "security"`</td></tr><tr><td><code>apt list --upgradable</code></td><td>Lists available updates for all packages, including security patches, on Debian/Ubuntu systems.</td></tr><tr><td><code>apt-get changelog &#x3C;package_name></code></td><td>View detailed changelog for a specific package on Debian/Ubuntu systems.</td></tr></tbody></table>

### <mark style="color:purple;">Red Hat/CentOS</mark>

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td>`rpm -qa</td><td>grep kernel`</td></tr><tr><td><code>yum check-update</code></td><td>Checks for available updates, including security patches, on Red Hat/CentOS systems.</td></tr><tr><td><code>yum updateinfo list security</code></td><td>Lists available security updates on Red Hat/CentOS systems.</td></tr><tr><td>`yum updateinfo list updates</td><td>grep security`</td></tr></tbody></table>

### <mark style="color:purple;">SUSE</mark>

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>zypper list-patches</code></td><td>Lists installed patches on SUSE systems.</td></tr><tr><td><code>zypper patch-info &#x3C;patch_number></code></td><td>View details about a specific patch on SUSE systems.</td></tr><tr><td><code>zypper patches --category security</code></td><td>Lists only security-related patches on SUSE systems.</td></tr></tbody></table>

## <mark style="color:purple;">Kernel Version Check</mark>

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>uname -r</code></td><td>Displays the current kernel version.</td></tr></tbody></table>

Compare this version with official release notes or online resources to identify applied hotfixes.&#x20;

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

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>ksplice</code></td><td>(Oracle Linux): Manages live kernel patching without reboots.</td></tr></tbody></table>

Third-party tools (e.g., `yum-plugin-security`, `zypper-patch-viewer`) might provide additional hotfix-related functionality.
