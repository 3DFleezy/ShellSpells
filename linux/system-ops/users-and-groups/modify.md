# Modify

## <mark style="color:red;">User Accounts</mark>

### <mark style="color:purple;">Account Management</mark>

<table data-full-width="true"><thead><tr><th width="312">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>passwd &#x3C;username></code></td><td>Change user password (requires root privileges).</td></tr><tr><td><code>useradd &#x3C;username></code></td><td>Create a new user account (requires root privileges).</td></tr><tr><td><code>userdel &#x3C;username></code></td><td>Delete an existing user account (requires root privileges).</td></tr><tr><td><code>usermod &#x3C;username></code></td><td>Modify various user account settings (requires root privileges).</td></tr><tr><td><code>chfn &#x3C;options> &#x3C;username></code></td><td>Changes the user's finger information (real name, office, phone, etc.).</td></tr><tr><td><code>chsh &#x3C;options> &#x3C;username></code></td><td>Changes the user's login shell.</td></tr><tr><td><code>passwd -l &#x3C;username></code></td><td>Lock a user account, preventing login (requires root privileges).</td></tr><tr><td><code>passwd -u &#x3C;username></code></td><td>Unlock a locked user account (requires root privileges).</td></tr><tr><td><code>usermod -L &#x3C;username></code></td><td>Disable a user account (requires root privileges).</td></tr><tr><td><code>usermod -U &#x3C;username></code></td><td>Enable a disabled user account (requires root privileges).</td></tr></tbody></table>

Example:\
`sudo useradd -m -d /home/username -s /bin/bash username`

`-m`: Creates the user's home directory as specified by the -d option. \
If -d is not specified with -m, the home directory is created under the location specified in /etc/default/useradd or the default /home/username. \
`-d /home/username`: Specifies the home directory for the new user. \
`-s /bin/bash`: Sets the default shell for the user.



### <mark style="color:purple;">Managing Group Membership</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="434">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>usermod -G &#x3C;group1>,&#x3C;group2> &#x3C;username></code></td><td>Add/Remove user from specific groups (requires root privileges).</td></tr><tr><td><code>groups &#x3C;username></code></td><td>Check user's current group memberships.</td></tr><tr><td><code>usermod -aG &#x3C;groupname> &#x3C;username></code></td><td>Adds a user to a group.</td></tr></tbody></table>



### <mark style="color:purple;">Password Policies</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="436">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>chapw</code></td><td>Manage system-wide password policies (requires root privileges).</td></tr><tr><td><code>chage -l &#x3C;username></code></td><td>Display password expiration info for user (requires root privileges).</td></tr><tr><td><code>chage &#x3C;options> &#x3C;username></code></td><td>Changes user password expiry info.</td></tr></tbody></table>



## <mark style="color:red;">Groups</mark>

### <mark style="color:purple;">Group Management</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="433">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>groupadd &#x3C;groupname></code></td><td>Creates a new group.</td></tr><tr><td><code>groupdel &#x3C;groupname></code></td><td>Deletes a group.</td></tr><tr><td><code>groupmod &#x3C;options> &#x3C;groupname></code></td><td>Modifies a group's name or GID (Group ID).</td></tr><tr><td><code>gpasswd &#x3C;options> &#x3C;groupname></code></td><td>Administers the <code>/etc/group</code> and <code>/etc/gshadow</code> files.</td></tr><tr><td><code>usermod -aG &#x3C;groupname> &#x3C;username></code></td><td>Adds a user to a group. <code>-aG</code> appends the user to the supplemental groups.</td></tr><tr><td><code>vigr</code></td><td>Edits the <code>/etc/group</code> file in a safe manner, similar to using <code>vipw</code>.</td></tr><tr><td><code>vigr -s</code></td><td>Edits the <code>/etc/gshadow</code> file in a safe manner, managing secure group account information.</td></tr></tbody></table>



### <mark style="color:purple;">Editing Config Files Directly</mark>

While you can use commands like `useradd`, `userdel`, `usermod`, and `passwd` for user management, direct editing of /etc/passwd and /etc/shadow is sometimes necessary for manual adjustments. \
It's recommended to use `vipw` and `vipw -s` for editing these files to prevent file corruption and maintain system security. Always back up these files before making direct edits.
