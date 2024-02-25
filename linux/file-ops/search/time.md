# Time

{% hint style="danger" %}
The find commands require root!!
{% endhint %}

<mark style="color:yellow;">`m`</mark> = Modification time \
<mark style="color:yellow;">`a`</mark> = Accessed time \
<mark style="color:yellow;">`c`</mark> = Change time (metadata changed). Includes changes to permissions or ownership. \
<mark style="color:yellow;">`Bt`</mark>= Birth time. Some Unix systems support this, such as MacOS.



## <mark style="color:red;">Accessed Time</mark>

Today (Starting at 00:00):

```bash
find / -a -daystart -atime -1
```

### <mark style="color:purple;">Days</mark>

| <mark style="color:yellow;">`find / -a -atime 10`</mark>            | Accessed \*EXACTLY 10 days ago       |
| ------------------------------------------------------------------- | ------------------------------------ |
| <mark style="color:yellow;">`find / -a -atime 0`</mark>             | Accessed within the last 24 hours    |
| <mark style="color:yellow;">`find / -a -atime 1`</mark>             | Accessed between 24 and 48 hours ago |
| <mark style="color:yellow;">`find / -a -atime -10`</mark>           | Accessed within the last 10 days     |
| <mark style="color:yellow;">`find / -a -atime +10`</mark>           | Accessed 10 or more days ago         |
| <mark style="color:yellow;">`find / -a -atime -10 -atime -5`</mark> | Accessed within the last 5-10 days   |

### <mark style="color:purple;">Hours</mark>

| <mark style="color:yellow;">`find / -a -amin -60`</mark>              | Accessed within the last hour (60 minutes) |
| --------------------------------------------------------------------- | ------------------------------------------ |
| <mark style="color:yellow;">`find / -a -amin -$((5*60))`</mark>       | Accessed within the last 5 hours           |
| <mark style="color:yellow;">`find / -a -atime 0`</mark>               | Accessed within the last 24 hours          |
| <mark style="color:yellow;">`find / -a -atime 1`</mark>               | Accessed between 24 and 48 hours ago       |
| <mark style="color:yellow;">`find / -a -atime -120 -atime -60`</mark> | Accessed within the last 60-120 minutes    |

### <mark style="color:purple;">Minutes</mark>

| <mark style="color:yellow;">`find / -a -amin -60`</mark>              | Accessed within the last hour (60 minutes) |
| --------------------------------------------------------------------- | ------------------------------------------ |
| <mark style="color:yellow;">`find / -a -amin -$((5*60))`</mark>       | Accessed within the last 5 hours           |
| <mark style="color:yellow;">`find / -a -atime 0`</mark>               | Accessed within the last 24 hours          |
| <mark style="color:yellow;">`find / -a -atime 1`</mark>               | Accessed between 24 and 48 hours ago       |
| <mark style="color:yellow;">`find / -a -atime -120 -atime -60`</mark> | Accessed within the last 60-120 minutes    |

### <mark style="color:purple;">Dates / Date Range</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="589">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -newerat "YYYY-MM-DD"</code></mark></td><td>Accessed after date</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newermt "YYYY-MM-DD"</code></mark></td><td>Accessed before date</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newerat 2017-09-12 ! -newerat 2017-09-14</code></mark></td><td>13 SEP access times only</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newerat 2017-09-12 ! -newerat 2017-09-19</code></mark></td><td>13 - 18 SEP access times only</td></tr></tbody></table>

### <mark style="color:purple;">Specific Hours on a Specific Date</mark>

Suppose you want to find files modified on February 10, 2024, and accessed between 3 PM and 4 PM on that same day.

Step 1: Create Reference Files for Modification Date&#x20;

First, create reference files to cover the entire day of February 10, 2024, for the modification date:&#x20;

Start of the day: February 10, 2024, 00:00 \
<mark style="color:yellow;">`touch -t 202402100000 start_day.tmp`</mark>

End of the day: February 11, 2024, 00:00\
<mark style="color:yellow;">`touch -t 202402110000 end_day.tmp`</mark>

Step 2: Create Reference Files for Access Time&#x20;

Next, create reference files for the hour you're interested in (3 PM to 4 PM):

{% code overflow="wrap" %}
```bash
find /path/to/search -type f \( -newermt @$(stat -c %Y start_day.tmp) ! -newermt @$(stat -c %Y end_day.tmp) \) -a \( -newerat @$(stat -c %Y start_hour.tmp) ! -newerat @$(stat -c %Y end_hour.tmp) \)
```
{% endcode %}

The <mark style="color:yellow;">`-a`</mark> operator ensures both conditions must be met for a file to match.\
<mark style="color:yellow;">`stat -c %Y filename.tmp`</mark> retrieves the modification time of each reference file in seconds since the epoch, which find then uses for comparison.

### <mark style="color:purple;">Reference File</mark>

<mark style="color:yellow;">`-newerXY [referencefile]`</mark>\
Succeeds if timestamp X of the file being considered is newer than timestamp Y of the file reference. \
X = The files being compared. \
Y = Reference File timestamp of choice. \
The letters X and Y can be any of the following letters:

<mark style="color:yellow;">`a`</mark> The access time of the file reference \
<mark style="color:yellow;">`B`</mark> The birth time of the file reference \
<mark style="color:yellow;">`c`</mark> The inode status change time of reference \
<mark style="color:yellow;">`m`</mark> The modification time of the file reference \
<mark style="color:yellow;">`t`</mark> reference is interpreted directly as a time

<table data-header-hidden data-full-width="true"><thead><tr><th width="435">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -newerat /reference_file</code></mark></td><td>Accessed after reference file</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newerat /reference_file</code></mark></td><td>Accessed before reference file</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newerma /reference_file</code></mark></td><td>Modified after the reference file's access time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newerma /reference_file</code></mark></td><td>Modified before the reference file's access time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newerca /reference_file</code></mark></td><td>Metadata Changed after the reference file's access time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newerca /reference_file</code></mark></td><td>Metadata Changed before the reference file's access time</td></tr></tbody></table>

## <mark style="color:red;">Modified Time</mark>

Today (Starting at 00:00):

```bash
find / -a -daystart -mtime -1
```

### <mark style="color:purple;">Days</mark>

| <mark style="color:yellow;">`find / -a -mtime 10`</mark>            | Modified \*EXACTLY 10 days ago       |
| ------------------------------------------------------------------- | ------------------------------------ |
| <mark style="color:yellow;">`find / -a -mtime 0`</mark>             | Modified within the last 24 hours    |
| <mark style="color:yellow;">`find / -a -mtime 1`</mark>             | Modified between 24 and 48 hours ago |
| <mark style="color:yellow;">`find / -a -mtime -10`</mark>           | Modified within the last 10 days     |
| <mark style="color:yellow;">`find / -a -mtime +10`</mark>           | Modified 10 or more days ago         |
| <mark style="color:yellow;">`find / -a -mtime -10 -mtime -5`</mark> | Modified within the last 5-10 days   |

### <mark style="color:purple;">Hours</mark>

| <mark style="color:yellow;">`find / -a -mmin -60`</mark>              | Modified within the last hour (60 minutes) |
| --------------------------------------------------------------------- | ------------------------------------------ |
| <mark style="color:yellow;">`find / -a -mmin -$((5*60))`</mark>       | Modified within the last 5 hours           |
| <mark style="color:yellow;">`find / -a -mtime 0`</mark>               | Modified within the last 24 hours          |
| <mark style="color:yellow;">`find / -a -mtime 1`</mark>               | Modified between 24 and 48 hours ago       |
| <mark style="color:yellow;">`find / -a -mtime -120 -mtime -60`</mark> | Modified within the last 60-120 minutes    |

### <mark style="color:purple;">Minutes</mark>

| <mark style="color:yellow;">`find / -a -mmin 10`</mark>           | Modified \*EXACTLY 10 minutes ago. Within that 60 seconds of 10 minutes ago. |
| ----------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| <mark style="color:yellow;">`find / -a -mmin -10`</mark>          | Modified within the last 10 minutes                                          |
| <mark style="color:yellow;">`find / -a -mmin +10`</mark>          | Modified 10 or more minutes ago                                              |
| <mark style="color:yellow;">`find / -a -mmin -10 -mmin -5`</mark> | Modified within the last 5-10 minutes                                        |

### <mark style="color:purple;">Dates / Date Range</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -newermt "YYYY-MM-DD"</code></mark></td><td>Modified after date</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newermt "YYYY-MM-DD"</code></mark></td><td>Modified before date</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newermt 2017-09-12 ! -newermt 2017-09-14</code></mark></td><td>13 SEP modify times only.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newermt 2017-09-12 ! -newermt 2017-09-19</code></mark></td><td>13 - 18 SEP modify times only</td></tr></tbody></table>

### <mark style="color:purple;">Specific Hours on a Specific Date</mark>

Step 1: Create Reference Files Start of the range: February 10, 2024, 15:00\
<mark style="color:yellow;">`touch -t 202402101500 start.tmp`</mark>

End of the range: February 10, 2024, 16:00\
<mark style="color:yellow;">`touch -t 202402101600 end.tmp`</mark>

Step 2: Use find to Search Within the Time Range

{% code overflow="wrap" %}
```bash
find / -a -type f -newermt @$(stat -c %Y start.tmp) ! -newermt @$(stat -c %Y end.tmp)
```
{% endcode %}

### <mark style="color:purple;">Reference File</mark>

<mark style="color:yellow;">`-newerXY [referencefile]`</mark>\
Succeeds if timestamp X of the file being considered is newer than timestamp Y of the file reference. \
X = The files being compared. \
Y = Reference File timestamp of choice. \
The letters X and Y can be any of the following letters:

<mark style="color:yellow;">`a`</mark> The access time of the file reference \
<mark style="color:yellow;">`B`</mark> The birth time of the file reference \
<mark style="color:yellow;">`c`</mark> The inode status change time of reference \
<mark style="color:yellow;">`m`</mark> The modification time of the file reference \
<mark style="color:yellow;">`t`</mark> reference is interpreted directly as a time

<table data-header-hidden data-full-width="true"><thead><tr><th width="440">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -newermt /reference_file</code></mark></td><td>Modified after reference file</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newermt /reference_file</code></mark></td><td>Modified before reference file</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -neweram /reference_file</code></mark></td><td>Modified after the reference file's modify time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -neweram /reference_file</code></mark></td><td>Modified before the reference file's modify time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newercm /reference_file</code></mark></td><td>Metadata Changed after the reference file's modify time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newercm /reference_file</code></mark></td><td>Metadata Changed before the reference file's modify time</td></tr></tbody></table>

## <mark style="color:red;">Change Time (Metadata Change)</mark>

Today (Starting at 00:00):

```sh
find / -a -daystart -ctime -1
```

### <mark style="color:purple;">Days</mark>

| <mark style="color:yellow;">`find / -a -ctime 10`</mark>            | Metadata changed \*EXACTLY 10 days ago. Meaning within the full 24 hours of the day, 10 days ago. |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| <mark style="color:yellow;">`find / -a -ctime 0`</mark>             | Metadata changed within the last 24 hours                                                         |
| <mark style="color:yellow;">`find / -a -ctime 1`</mark>             | Metadata changed between 24 and 48 hours ago                                                      |
| <mark style="color:yellow;">`find / -a -ctime -10`</mark>           | Metadata changed within the last 10 days                                                          |
| <mark style="color:yellow;">`find / -a -ctime +10`</mark>           | Metadata changed 10 or more days ago                                                              |
| <mark style="color:yellow;">`find / -a -ctime -10 -ctime -5`</mark> | Metadata changed within the last 5-10 days                                                        |

### <mark style="color:purple;">Hours</mark>

| <mark style="color:yellow;">`find / -a -cmin -60`</mark>              | Metadata changed within the last hour (60 minutes) |
| --------------------------------------------------------------------- | -------------------------------------------------- |
| <mark style="color:yellow;">`find / -a -cmin -$((5*60))`</mark>       | Metadata changed within the last 5 hours           |
| <mark style="color:yellow;">`find / -a -ctime 0`</mark>               | Metadata changed within the last 24 hours          |
| <mark style="color:yellow;">`find / -a -ctime 1`</mark>               | Metadata changed between 24 and 48 hours ago       |
| <mark style="color:yellow;">`find / -a -ctime -120 -ctime -60`</mark> | Metadata changed within the last 60-120 minutes    |

### <mark style="color:purple;">Minutes</mark>

| <mark style="color:yellow;">`find / -a -cmin 10`</mark>           | Metadata changed _exactly_ 10 minutes ago. Within that 60 seconds of 10 minutes ago. |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| <mark style="color:yellow;">`find / -a -cmin -10`</mark>          | Metadata changed within the last 10 minutes                                          |
| <mark style="color:yellow;">`find / -a -cmin +10`</mark>          | Metadata changed 10 or more minutes ago                                              |
| <mark style="color:yellow;">`find / -a -cmin -10 -cmin -5`</mark> | Metadata changed within the last 5-10 minutes                                        |

### <mark style="color:purple;">Dates / Date Range</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="569">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -newerct "YYYY-MM-DD"</code></mark></td><td>Metadata Changed after date</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newerct "YYYY-MM-DD"</code></mark></td><td>Metadata changed before date</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newerct 2017-09-12 ! -newerct 2017-09-14</code></mark></td><td>13 SEP metadata change times only</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newerct 2017-09-12 ! -newerct 2017-09-19</code></mark></td><td>13 - 18 SEP metadata change times only</td></tr></tbody></table>

### <mark style="color:purple;">Specific Hours on a Specific Date</mark>

Suppose you're looking for files that were modified on February 10, 2024, and had their metadata changed between 3 PM and 4 PM on the same day.

Step 1: Create Reference Files for Modification Date You'll create two reference files to cover the entire day of February 10, 2024: \
Start of the day: February 10, 2024, 00:00\
<mark style="color:yellow;">`touch -t 202402100000 start_day.tmp`</mark>

End of the day: February 11, 2024, 00:00\
<mark style="color:yellow;">`touch -t 202402110000 end_day.tmp`</mark>

Step 2: Create Reference Files for Change Time \
Next, create reference files for the hour you're interested in (3 PM to 4 PM): \
Start of the range: February 10, 2024, 15:00\
<mark style="color:yellow;">`touch -t 202402101500 start_hour.tmp`</mark>

End of the range: February 10, 2024, 16:00\
<mark style="color:yellow;">`touch -t 202402101600 end_hour.tmp`</mark>

Step 3: Use find to Search Within the Time Range

{% code overflow="wrap" %}
```bash
find / -a -type f \( -newermt @$(stat -c %Y start_day.tmp) ! -newermt @$(stat -c %Y end_day.tmp) \) -a \( -newerct @$(stat -c %Y start_hour.tmp) ! -newerct @$(stat -c %Y end_hour.tmp) \)
```
{% endcode %}

The <mark style="color:yellow;">`-a`</mark> operator is used to ensure both conditions must be met. \
The <mark style="color:yellow;">`stat -c %Y`</mark> command fetches the modification time in seconds since the epoch, which is then used by find for comparison.

{% hint style="warning" %}
Remember: ctime changes for many reasons beyond just metadata changes, including modifications to the file itself
{% endhint %}

### <mark style="color:purple;">Reference File</mark>

<mark style="color:yellow;">`-newerXY [referencefile]`</mark>\
&#x20;Succeeds if timestamp X of the file being considered is newer than timestamp Y of the file reference. \
X = The files being compared. \
Y = Reference File timestamp of choice. \
The letters X and Y can be any of the following letters:

<mark style="color:yellow;">`a`</mark> The access time of the file reference \
<mark style="color:yellow;">`B`</mark> The birth time of the file reference \
<mark style="color:yellow;">`c`</mark> The inode status change time of reference \
<mark style="color:yellow;">`m`</mark> The modification time of the file reference \
<mark style="color:yellow;">`t`</mark> reference is interpreted directly as a time

<table data-header-hidden data-full-width="true"><thead><tr><th width="424">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -newerct /reference_file</code></mark></td><td>Modified after reference file</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newerct /reference_file</code></mark></td><td>Modified before reference file</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newerac /reference_file</code></mark></td><td>Accessed after the reference file's Metadata Change time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newerac /reference_file</code></mark></td><td>Accessed before the reference file's Metadata Change time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -newermc /reference_file</code></mark></td><td>Modified after the reference file's Metadata Change time</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -newermc /reference_file</code></mark></td><td>Modified before the reference file's Metadata Change time</td></tr></tbody></table>

## <mark style="color:red;">Birth Time</mark>

Not supported on all systems (including kali) \
<mark style="color:yellow;">`-newerBt`</mark>
