# Inode

| Command                                | Description                                   |
| -------------------------------------- | --------------------------------------------- |
| `ls -li`                               | Shows file inode numbers                      |
| `find / -a -inum 74653`                | Find all files with associated inode number   |
| `find / -a -samefile /usr/bin/dispuid` | Find all files that are the same (same inode) |

Find file by its inode number.

{% hint style="danger" %}
Use with caution. This method allows modifying the raw filesystem data.
{% endhint %}

```bash
debugfs /dev/<filesystem> ls -i <inode_number>
```
