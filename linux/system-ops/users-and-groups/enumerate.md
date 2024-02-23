# Enumerate

## <mark style="color:red;">Current User</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="294">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>whoami</code></td><td>Displays the user name of the user running the command.</td></tr><tr><td><code>sudo -l</code></td><td>May be configured to allow users to run some commands with root privileges.</td></tr><tr><td><code>id</code></td><td>Shows a user's privileges and group membership.</td></tr><tr><td><code>groups</code></td><td>Displays the current user's groups.</td></tr><tr><td><code>finger</code></td><td>Provides detailed information for the current user (if installed).</td></tr><tr><td><code>logname</code></td><td>Shows the username of the user who initiated the session.</td></tr><tr><td><code>env</code></td><td>Lists all environment variables associated with the current user's shell session.</td></tr><tr><td><code>echo $USER</code></td><td>Prints the username.</td></tr><tr><td><code>echo $HOME</code></td><td>Displays the user's home directory path.</td></tr><tr><td><code>echo $SHELL</code></td><td>Shows the user's default login shell.</td></tr><tr><td><code>history</code></td><td>Displays previously executed commands from the last terminal session.</td></tr></tbody></table>



## <mark style="color:red;">All Users</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="311">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>cat /etc/passwd</code></td><td>Lists user accounts.</td></tr><tr><td><code>grep &#x3C;pattern> /etc/passwd</code></td><td>Search /etc/password for pattern.</td></tr><tr><td><code>id &#x3C;username></code></td><td>Shows user and group IDs for a user.</td></tr><tr><td><code>finger &#x3C;username></code></td><td>Provides user details (may not be installed by default).</td></tr><tr><td><code>users</code></td><td>Displays logged-in users.</td></tr><tr><td><code>who</code></td><td>Display currently logged-in users.</td></tr><tr><td><code>w</code></td><td>Display who is logged in and what they are doing.</td></tr><tr><td><code>last</code></td><td>Lists last logged-in users (/var/log/wtmp).</td></tr><tr><td><code>lastb</code></td><td>List last bad login attempts (/var/log/btmp).</td></tr><tr><td><code>lastlog</code></td><td>Shows the last login time for users.</td></tr><tr><td><code>cat /etc/sudoers</code></td><td>Display sudo configuration.</td></tr><tr><td><code>groups &#x3C;username></code></td><td>Lists groups for a user.</td></tr><tr><td><code>compgen -u</code></td><td>Lists usernames (bash built-in).</td></tr><tr><td><code>getent passwd</code></td><td>Entries from passwd database similar to /etc/passwd, but includes network-based user databases.</td></tr><tr><td><code>passwd -s &#x3C;username></code></td><td>Info about a user's password status (locked, expired, etc.) (requires root privileges).</td></tr></tbody></table>

Extract just usernames from the /etc/passwd file:

{% code fullWidth="false" %}
```bash
awk -F ':' '{print $1}' /etc/passwd
```
{% endcode %}



## <mark style="color:red;">Groups</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="304">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>cat /etc/group</code></td><td>Lists groups.</td></tr><tr><td><code>cat /etc/sudoers</code></td><td>Sudo configuration.</td></tr><tr><td><code>groups</code></td><td>Current user's groups.</td></tr><tr><td><code>groups &#x3C;username></code></td><td>Lists groups for a user.</td></tr><tr><td><code>compgen -g</code></td><td>Lists group names (bash built-in).</td></tr><tr><td><code>id</code></td><td>Shows the current user's group IDs.</td></tr><tr><td><code>id &#x3C;username></code></td><td>Shows the user's group IDs for a specific user.</td></tr><tr><td><code>grep &#x3C;pattern> /etc/group</code></td><td>Search /etc/groups by patterns.</td></tr><tr><td><code>getent group</code></td><td>Group entries from databases similar to /etc/group, but includes network-based group databases.</td></tr></tbody></table>

Extract just group names from the /etc/group file:

```bash
awk -F ':' '{print $1}' /etc/group
```
