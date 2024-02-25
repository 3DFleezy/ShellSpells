# Modify

## <mark style="color:red;">User Accounts</mark>

### <mark style="color:purple;">Account Management</mark>

<table data-full-width="true"><thead><tr><th width="312">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>passwd &#x3C;username></code></mark></td><td>Change user password (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>useradd &#x3C;username></code></mark></td><td>Create a new user account (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>userdel &#x3C;username></code></mark></td><td>Delete an existing user account (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>usermod &#x3C;username></code></mark></td><td>Modify various user account settings (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>chfn &#x3C;options> &#x3C;username></code></mark></td><td>Changes the user's finger information (real name, office, phone, etc.).</td></tr><tr><td><mark style="color:yellow;"><code>chsh &#x3C;options> &#x3C;username></code></mark></td><td>Changes the user's login shell.</td></tr><tr><td><mark style="color:yellow;"><code>passwd -l &#x3C;username></code></mark></td><td>Lock a user account, preventing login (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>passwd -u &#x3C;username></code></mark></td><td>Unlock a locked user account (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>usermod -L &#x3C;username></code></mark></td><td>Disable a user account (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>usermod -U &#x3C;username></code></mark></td><td>Enable a disabled user account (requires root privileges).</td></tr></tbody></table>

Example:\
<mark style="color:yellow;">`sudo useradd -m -d /home/username -s /bin/bash username`</mark>

<mark style="color:yellow;">`-m`</mark>: Creates the user's home directory as specified by the -d option.\
If -d is not specified with -m, the home directory is created under the location specified in /etc/default/useradd or the default /home/username.\
<mark style="color:yellow;">`-d /home/username`</mark>: Specifies the home directory for the new user.\
<mark style="color:yellow;">`-s /bin/bash`</mark>: Sets the default shell for the user.

### <mark style="color:purple;">Managing Group Membership</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="434">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>usermod -G &#x3C;group1>,&#x3C;group2> &#x3C;username></code></mark></td><td>Add/Remove user from specific groups (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>groups &#x3C;username></code></mark></td><td>Check user's current group memberships.</td></tr><tr><td><mark style="color:yellow;"><code>usermod -aG &#x3C;groupname> &#x3C;username></code></mark></td><td>Adds a user to a group.</td></tr></tbody></table>

### <mark style="color:purple;">Password Policies</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="436">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>chapw</code></mark></td><td>Manage system-wide password policies (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>chage -l &#x3C;username></code></mark></td><td>Display password expiration info for user (requires root privileges).</td></tr><tr><td><mark style="color:yellow;"><code>chage &#x3C;options> &#x3C;username></code></mark></td><td>Changes user password expiry info.</td></tr></tbody></table>

## <mark style="color:red;">Groups</mark>

### <mark style="color:purple;">Group Management</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="433">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>groupadd &#x3C;groupname></code></mark></td><td>Creates a new group.</td></tr><tr><td><mark style="color:yellow;"><code>groupdel &#x3C;groupname></code></mark></td><td>Deletes a group.</td></tr><tr><td><mark style="color:yellow;"><code>groupmod &#x3C;options> &#x3C;groupname></code></mark></td><td>Modifies a group's name or GID (Group ID).</td></tr><tr><td><mark style="color:yellow;"><code>gpasswd &#x3C;options> &#x3C;groupname></code></mark></td><td>Administers the <mark style="color:yellow;"><code>/etc/group</code></mark> and <mark style="color:yellow;"><code>/etc/gshadow</code></mark> files.</td></tr><tr><td><mark style="color:yellow;"><code>usermod -aG &#x3C;groupname> &#x3C;username></code></mark></td><td>Adds a user to a group. <mark style="color:yellow;"><code>-aG</code></mark> appends the user to the supplemental groups.</td></tr><tr><td><mark style="color:yellow;"><code>vigr</code></mark></td><td>Edits the <mark style="color:yellow;"><code>/etc/group</code></mark> file in a safe manner, similar to using <code>vipw</code>.</td></tr><tr><td><mark style="color:yellow;"><code>vigr -s</code></mark></td><td>Edits the <mark style="color:yellow;"><code>/etc/gshadow</code></mark> file in a safe manner, managing secure group account information.</td></tr></tbody></table>

### <mark style="color:purple;">Editing Config Files Directly</mark>

While you can use commands like <mark style="color:yellow;">`useradd`</mark>, <mark style="color:yellow;">`userdel`</mark>, <mark style="color:yellow;">`usermod`</mark>, and <mark style="color:yellow;">`passwd`</mark> for user management, direct editing of /etc/passwd and /etc/shadow is sometimes necessary for manual adjustments.\
It's recommended to use <mark style="color:yellow;">`vipw`</mark> and <mark style="color:yellow;">`vipw -s`</mark> for editing these files to prevent file corruption and maintain system security. Always back up these files before making direct edits.
