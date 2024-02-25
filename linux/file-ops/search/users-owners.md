# Users (Owners)

<table data-header-hidden data-full-width="true"><thead><tr><th width="546">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -user [username]</code></mark></td><td>Owned by user</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -user [username]</code></mark></td><td>Not owned by user</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -group [groupname]</code></mark></td><td>Group name</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user "root:developers"</code></mark></td><td>Owned by root AND belong to developers group</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user root -o -group root</code></mark></td><td>Owned by root OR belong to root group</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user1 [username1] -o -user2 [username2]</code></mark></td><td>Multiple owners (username1 OR username2)</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user "([username1]|[username2])"</code></mark></td><td>Multiple owners (username1 OR username2)</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -nouser -exec ls -l {} \;</code></mark></td><td>No owner</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -nogroup -exec ls -l {} \;</code></mark></td><td>No group</td></tr><tr><td><mark style="color:yellow;"><code>sudo -u [username] find / -user [username]</code></mark></td><td>Executes <mark style="color:yellow;"><code>find</code></mark> as <mark style="color:yellow;"><code>&#x3C;username></code></mark></td></tr></tbody></table>

Recursively lists file ACLs and filters for entries related to <mark style="color:yellow;">`[username]`</mark>.\
This can be useful for systems using ACLs for finer-grained permissions:

```bash
getfacl -R [directory] | grep "user:[username]"
```

Lists files and directories in <mark style="color:yellow;">`[directory]`</mark> with detailed information and filters the output for those owned by <mark style="color:yellow;">`[username]`</mark>.

{% hint style="warning" %}
Note: This method is less reliable and more cumbersome than using `find`.\
This is more of a last resort option:
{% endhint %}

```bash
` ls -l [directory] | grep '^.\{8\}[username]'
```
