---
description: Find files based on size
---

# Size

<mark style="color:yellow;">`c`</mark> bytes\
<mark style="color:yellow;">`k`</mark> kilobytes\
<mark style="color:yellow;">`M`</mark> megabytes\
<mark style="color:yellow;">`G`</mark> gigabytes\
<mark style="color:yellow;">`w`</mark> 2-byte words\
<mark style="color:yellow;">`b`</mark> 512-byte blocks

| <mark style="color:yellow;">`find / -a -size 10c`</mark>             | Exactly 10 bytes             |
| -------------------------------------------------------------------- | ---------------------------- |
| <mark style="color:yellow;">`find / -a -size +10k`</mark>            | More than 10 kilobytes       |
| <mark style="color:yellow;">`find / -a -size -10M`</mark>            | Less than 10 megabytes       |
| <mark style="color:yellow;">`find / -a -size 0c`</mark>              | Empty files (size 0 bytes).  |
| <mark style="color:yellow;">`find / -a -size +10M -size -50M`</mark> | Between 10 and 50 megabytes. |

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
