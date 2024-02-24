# Time

{% hint style="danger" %}
The find commands require root!!
{% endhint %}

`m` = Modification time \
`a` = Accessed time \
`c` = Change time (metadata changed). Includes changes to permissions or ownership. \
`Bt`= Birth time. Some Unix systems support this, such as MacOS.



## Accessed Time

Today (Starting at 00:00): \` find / -a -daystart -atime -1

### Days

| Command                          | Description                          |
| -------------------------------- | ------------------------------------ |
| `find / -a -atime 10`            | Accessed \*EXACTLY 10 days ago       |
| `find / -a -atime 0`             | Accessed within the last 24 hours    |
| `find / -a -atime 1`             | Accessed between 24 and 48 hours ago |
| `find / -a -atime -10`           | Accessed within the last 10 days     |
| `find / -a -atime +10`           | Accessed 10 or more days ago         |
| `find / -a -atime -10 -atime -5` | Accessed within the last 5-10 days   |

### Hours

| Command                            | Description                                |
| ---------------------------------- | ------------------------------------------ |
| `find / -a -amin -60`              | Accessed within the last hour (60 minutes) |
| `find / -a -amin -$((5*60))`       | Accessed within the last 5 hours           |
| `find / -a -atime 0`               | Accessed within the last 24 hours          |
| `find / -a -atime 1`               | Accessed between 24 and 48 hours ago       |
| `find / -a -atime -120 -atime -60` | Accessed within the last 60-120 minutes    |

### Minutes

| Command                        | Description                                                                  |
| ------------------------------ | ---------------------------------------------------------------------------- |
| `find / -a -amin 10`           | Accessed \*EXACTLY 10 minutes ago. Within that 60 seconds of 10 minutes ago. |
| `find / -a -amin -10`          | Accessed within the last 10 minutes                                          |
| `find / -a -amin +10`          | Accessed 10 or more minutes ago                                              |
| `find / -a -amin -10 -amin -5` | Accessed within the last 5-10 minutes                                        |

### Dates / Date Range

| Command                                               | Description                   |
| ----------------------------------------------------- | ----------------------------- |
| `find / -a -newerat "YYYY-MM-DD"`                     | Accessed after date           |
| `find / -a ! -newermt "YYYY-MM-DD"`                   | Accessed before date          |
| `find / -a -newerat 2017-09-12 ! -newerat 2017-09-14` | 13 SEP access times only      |
| `find / -a -newerat 2017-09-12 ! -newerat 2017-09-19` | 13 - 18 SEP access times only |

### Specific Hours on a Specific Date

Suppose you want to find files modified on February 10, 2024, and accessed between 3 PM and 4 PM on that same day.

Step 1: Create Reference Files for Modification Date&#x20;

First, create reference files to cover the entire day of February 10, 2024, for the modification date:&#x20;

Start of the day: February 10, 2024, 00:00 \
`touch -t 202402100000 start_day.tmp`

End of the day: February 11, 2024, 00:00\
`touch -t 202402110000 end_day.tmp`

Step 2: Create Reference Files for Access Time&#x20;

Next, create reference files for the hour you're interested in (3 PM to 4 PM):

{% code overflow="wrap" %}
```bash
find /path/to/search -type f \( -newermt @$(stat -c %Y start_day.tmp) ! -newermt @$(stat -c %Y end_day.tmp) \) -a \( -newerat @$(stat -c %Y start_hour.tmp) ! -newerat @$(stat -c %Y end_hour.tmp) \)
```
{% endcode %}

The `-a` operator ensures both conditions must be met for a file to match.\
`stat -c %Y filename.tmp` retrieves the modification time of each reference file in seconds since the epoch, which find then uses for comparison.

### Reference File

`-newerXY [referencefile]`\
Succeeds if timestamp X of the file being considered is newer than timestamp Y of the file reference. \
X = The files being compared. \
Y = Reference File timestamp of choice. \
The letters X and Y can be any of the following letters:

`a` The access time of the file reference \
`B` The birth time of the file reference \
`c` The inode status change time of reference \
`m` The modification time of the file reference \
`t` reference is interpreted directly as a time

<table data-header-hidden data-full-width="true"><thead><tr><th width="435">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>find / -a -newerat /reference_file</code></td><td>Accessed after reference file</td></tr><tr><td><code>find / -a ! -newerat /reference_file</code></td><td>Accessed before reference file</td></tr><tr><td><code>find / -a -newerma /reference_file</code></td><td>Modified after the reference file's access time</td></tr><tr><td><code>find / -a ! -newerma /reference_file</code></td><td>Modified before the reference file's access time</td></tr><tr><td><code>find / -a -newerca /reference_file</code></td><td>Metadata Changed after the reference file's access time</td></tr><tr><td><code>find / -a ! -newerca /reference_file</code></td><td>Metadata Changed before the reference file's access time</td></tr></tbody></table>

## Modified Time

Today (Starting at 00:00):\
`find / -a -daystart -mtime -1`

### Days

| Command                          | Description                          |
| -------------------------------- | ------------------------------------ |
| `find / -a -mtime 10`            | Modified \*EXACTLY 10 days ago       |
| `find / -a -mtime 0`             | Modified within the last 24 hours    |
| `find / -a -mtime 1`             | Modified between 24 and 48 hours ago |
| `find / -a -mtime -10`           | Modified within the last 10 days     |
| `find / -a -mtime +10`           | Modified 10 or more days ago         |
| `find / -a -mtime -10 -mtime -5` | Modified within the last 5-10 days   |

### Hours

| Command                            | Description                                |
| ---------------------------------- | ------------------------------------------ |
| `find / -a -mmin -60`              | Modified within the last hour (60 minutes) |
| `find / -a -mmin -$((5*60))`       | Modified within the last 5 hours           |
| `find / -a -mtime 0`               | Modified within the last 24 hours          |
| `find / -a -mtime 1`               | Modified between 24 and 48 hours ago       |
| `find / -a -mtime -120 -mtime -60` | Modified within the last 60-120 minutes    |

### Minutes

| Command                        | Description                                                                  |
| ------------------------------ | ---------------------------------------------------------------------------- |
| `find / -a -mmin 10`           | Modified \*EXACTLY 10 minutes ago. Within that 60 seconds of 10 minutes ago. |
| `find / -a -mmin -10`          | Modified within the last 10 minutes                                          |
| `find / -a -mmin +10`          | Modified 10 or more minutes ago                                              |
| `find / -a -mmin -10 -mmin -5` | Modified within the last 5-10 minutes                                        |

### Dates / Date Range

| Command                                               | Description                   |
| ----------------------------------------------------- | ----------------------------- |
| `find / -a -newermt "YYYY-MM-DD"`                     | Modified after date           |
| `find / -a ! -newermt "YYYY-MM-DD"`                   | Modified before date          |
| `find / -a -newermt 2017-09-12 ! -newermt 2017-09-14` | 13 SEP modify times only.     |
| `find / -a -newermt 2017-09-12 ! -newermt 2017-09-19` | 13 - 18 SEP modify times only |

### Specific Hours on a Specific Date

Step 1: Create Reference Files Start of the range: February 10, 2024, 15:00\
`touch -t 202402101500 start.tmp`

End of the range: February 10, 2024, 16:00\
`touch -t 202402101600 end.tmp`

Step 2: Use find to Search Within the Time Range

{% code overflow="wrap" %}
```bash
find / -a -type f -newermt @$(stat -c %Y start.tmp) ! -newermt @$(stat -c %Y end.tmp)
```
{% endcode %}

### Reference File

`-newerXY [referencefile]`\
Succeeds if timestamp X of the file being considered is newer than timestamp Y of the file reference. \
X = The files being compared. \
Y = Reference File timestamp of choice. \
The letters X and Y can be any of the following letters:

`a` The access time of the file reference \
`B` The birth time of the file reference \
`c` The inode status change time of reference \
`m` The modification time of the file reference \
`t` reference is interpreted directly as a time

| Command                                | Description                                              |
| -------------------------------------- | -------------------------------------------------------- |
| `find / -a -newermt /reference_file`   | Modified after reference file                            |
| `find / -a ! -newermt /reference_file` | Modified before reference file                           |
| `find / -a -neweram /reference_file`   | Modified after the reference file's modify time          |
| `find / -a ! -neweram /reference_file` | Modified before the reference file's modify time         |
| `find / -a -newercm /reference_file`   | Metadata Changed after the reference file's modify time  |
| `find / -a ! -newercm /reference_file` | Metadata Changed before the reference file's modify time |

## Change Time (Metadata Change)

Today (Starting at 00:00):\
`find / -a -daystart -ctime -1`

### Days

| Command                          | Description                                                                                       |
| -------------------------------- | ------------------------------------------------------------------------------------------------- |
| `find / -a -ctime 10`            | Metadata changed \*EXACTLY 10 days ago. Meaning within the full 24 hours of the day, 10 days ago. |
| `find / -a -ctime 0`             | Metadata changed within the last 24 hours                                                         |
| `find / -a -ctime 1`             | Metadata changed between 24 and 48 hours ago                                                      |
| `find / -a -ctime -10`           | Metadata changed within the last 10 days                                                          |
| `find / -a -ctime +10`           | Metadata changed 10 or more days ago                                                              |
| `find / -a -ctime -10 -ctime -5` | Metadata changed within the last 5-10 days                                                        |

### Hours

| Command                            | Description                                        |
| ---------------------------------- | -------------------------------------------------- |
| `find / -a -cmin -60`              | Metadata changed within the last hour (60 minutes) |
| `find / -a -cmin -$((5*60))`       | Metadata changed within the last 5 hours           |
| `find / -a -ctime 0`               | Metadata changed within the last 24 hours          |
| `find / -a -ctime 1`               | Metadata changed between 24 and 48 hours ago       |
| `find / -a -ctime -120 -ctime -60` | Metadata changed within the last 60-120 minutes    |

### Minutes

| Command                        | Description                                                                          |
| ------------------------------ | ------------------------------------------------------------------------------------ |
| `find / -a -cmin 10`           | Metadata changed _exactly_ 10 minutes ago. Within that 60 seconds of 10 minutes ago. |
| `find / -a -cmin -10`          | Metadata changed within the last 10 minutes                                          |
| `find / -a -cmin +10`          | Metadata changed 10 or more minutes ago                                              |
| `find / -a -cmin -10 -cmin -5` | Metadata changed within the last 5-10 minutes                                        |

### Dates / Date Range

| Command                                               | Description                            |
| ----------------------------------------------------- | -------------------------------------- |
| `find / -a -newerct "YYYY-MM-DD"`                     | Metadata Changed after date            |
| `find / -a ! -newerct "YYYY-MM-DD"`                   | Metadata changed before date           |
| `find / -a -newerct 2017-09-12 ! -newerct 2017-09-14` | 13 SEP metadata change times only      |
| `find / -a -newerct 2017-09-12 ! -newerct 2017-09-19` | 13 - 18 SEP metadata change times only |

### Specific Hours on a Specific Date

Suppose you're looking for files that were modified on February 10, 2024, and had their metadata changed between 3 PM and 4 PM on the same day.

Step 1: Create Reference Files for Modification Date You'll create two reference files to cover the entire day of February 10, 2024: \
Start of the day: February 10, 2024, 00:00\
`touch -t 202402100000 start_day.tmp`

End of the day: February 11, 2024, 00:00\
`touch -t 202402110000 end_day.tmp`

Step 2: Create Reference Files for Change Time \
Next, create reference files for the hour you're interested in (3 PM to 4 PM): \
Start of the range: February 10, 2024, 15:00\
`touch -t 202402101500 start_hour.tmp`

End of the range: February 10, 2024, 16:00\
`touch -t 202402101600 end_hour.tmp`

Step 3: Use find to Search Within the Time Range

{% code overflow="wrap" %}
```bash
find / -a -type f \( -newermt @$(stat -c %Y start_day.tmp) ! -newermt @$(stat -c %Y end_day.tmp) \) -a \( -newerct @$(stat -c %Y start_hour.tmp) ! -newerct @$(stat -c %Y end_hour.tmp) \)
```
{% endcode %}

The `-a` operator is used to ensure both conditions must be met. \
The `stat -c %Y` command fetches the modification time in seconds since the epoch, which is then used by find for comparison.

{% hint style="warning" %}
Remember: ctime changes for many reasons beyond just metadata changes, including modifications to the file itself
{% endhint %}

### Reference File

`-newerXY [referencefile]`\
&#x20;Succeeds if timestamp X of the file being considered is newer than timestamp Y of the file reference. \
X = The files being compared. \
Y = Reference File timestamp of choice. \
The letters X and Y can be any of the following letters:

`a` The access time of the file reference \
`B` The birth time of the file reference \
`c` The inode status change time of reference \
`m` The modification time of the file reference \
`t` reference is interpreted directly as a time

| Command                                | Description                                               |
| -------------------------------------- | --------------------------------------------------------- |
| `find / -a -newerct /reference_file`   | Modified after reference file                             |
| `find / -a ! -newerct /reference_file` | Modified before reference file                            |
| `find / -a -newerac /reference_file`   | Accessed after the reference file's Metadata Change time  |
| `find / -a ! -newerac /reference_file` | Accessed before the reference file's Metadata Change time |
| `find / -a -newermc /reference_file`   | Modified after the reference file's Metadata Change time  |
| `find / -a ! -newermc /reference_file` | Modified before the reference file's Metadata Change time |

## Birth Time

Not supported on all systems (including kali) \
`-newerBt`
