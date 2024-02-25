# Inode

<table data-header-hidden data-full-width="true"><thead><tr><th width="405">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ls -li</code></td><td>Shows file inode numbers</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -inum 74653</code></td><td>Find all files with associated inode number</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -samefile /usr/bin/dispuid</code></td><td>Find all files that are the same (same inode)</td></tr></tbody></table>

Find file by its inode number.

{% hint style="danger" %}
Use with caution. This method allows modifying the raw filesystem data.
{% endhint %}

```bash
debugfs /dev/<filesystem> ls -i <inode_number>
```
