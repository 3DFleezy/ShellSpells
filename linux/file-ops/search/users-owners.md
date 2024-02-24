# Users (Owners)

<table data-header-hidden data-full-width="true"><thead><tr><th width="546">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>find / -a -user [username]</code></td><td>Owned by user</td></tr><tr><td><code>find / -a ! -user [username]</code></td><td>Not owned by user</td></tr><tr><td><code>find / -a -group [groupname]</code></td><td>Group name</td></tr><tr><td><code>find / -a -user "root:developers"</code></td><td>Owned by root AND belong to developers group</td></tr><tr><td><code>find / -a -user root -o -group root</code></td><td>Owned by root OR belong to root group</td></tr><tr><td><code>find / -a -user1 [username1] -o -user2 [username2]</code></td><td>Multiple owners (username1 OR username2)</td></tr><tr><td><code>find / -a -user "([username1]|[username2])"</code></td><td></td></tr><tr><td><code>find / -a -nouser -exec ls -l {} \;</code></td><td>No owner</td></tr><tr><td><code>find / -a -nogroup -exec ls -l {} \;</code></td><td>No group</td></tr><tr><td><code>sudo -u [username] find / -user [username]</code></td><td>Executes <code>find</code> as <code>&#x3C;username></code></td></tr></tbody></table>



Recursively lists file ACLs and filters for entries related to `[username]`.\
This can be useful for systems using ACLs for finer-grained permissions:

```bash
getfacl -R [directory] | grep "user:[username]"
```



Lists files and directories in `[directory]` with detailed information and filters the output for those owned by `[username]`.

{% hint style="warning" %}
Note: This method is less reliable and more cumbersome than using `find`.\
This is more of a last resort option:
{% endhint %}

```bash
` ls -l [directory] | grep '^.\{8\}[username]'
```
