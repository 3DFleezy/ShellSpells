---
description: Find files based on size
---

# Size

`c` bytes \
`k` kilobytes \
`M` megabytes \
`G` gigabytes \
`w` 2-byte words \
`b` 512-byte blocks

| Command                           | Description                  |
| --------------------------------- | ---------------------------- |
| `find / -a -size 10c`             | Exactly 10 bytes             |
| `find / -a -size +10k`            | More than 10 kilobytes       |
| `find / -a -size -10M`            | Less than 10 megabytes       |
| `find / -a -size 0c`              | Empty files (size 0 bytes).  |
| `find / -a -size +10M -size -50M` | Between 10 and 50 megabytes. |

Find large files:

```bash
find / -a -type f -size +100M -exec ls -lh {} \;
```

Find large directories:

```bash
find / -a -type d -size +1G -exec du -h --max-depth=1 {} \;
```

Finds files larger than the size of the current directory (using du to calculate total size):

```bash
find . -a -size $(du -sk * | awk '{print $1}')
```
