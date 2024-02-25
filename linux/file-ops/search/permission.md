# Permission

## <mark style="color:red;">Read</mark>

### <mark style="color:purple;">Other/World</mark>

| <mark style="color:yellow;">`find / -a -perm -o+r`</mark> | World-readable     |
| --------------------------------------------------------- | ------------------ |
| <mark style="color:yellow;">`find / -a -perm -4`</mark>   | World-readable     |
| <mark style="color:yellow;">`grep -r "r-." /`</mark>      | Alternative method |

Extracts usernames from /etc/passwd and finds files owned by each user where "others" have read permission (Need to test):

```bash
grep "r-" /etc/passwd | cut -d: -f1 | xargs find . -user
```

### <mark style="color:purple;">Current User</mark>

| <mark style="color:yellow;">`find / -a -readable`</mark>  | Current user readable. |
| --------------------------------------------------------- | ---------------------- |
| <mark style="color:yellow;">`find / -a -perm -u+r`</mark> | Current user readable. |

### <mark style="color:purple;">User specific</mark>

<table data-header-hidden data-full-width="false"><thead><tr><th width="419">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -readable</code></mark></td><td>Specific user readable.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -perm -4</code></mark></td><td>Specific user readable.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -perm -u+r</code></mark></td><td>Combines owner read permission to show files owned by user with read permissions.</td></tr></tbody></table>

### <mark style="color:purple;">Group</mark>

<table data-header-hidden><thead><tr><th width="444">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm -g+r</code></mark></td><td>Group readable.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -group &#x3C;group_name> -readable</code></mark></td><td>Specific group readable.</td></tr></tbody></table>

## <mark style="color:red;">Write</mark>

### <mark style="color:purple;">Other/World</mark>

<table data-header-hidden><thead><tr><th width="320">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm -o+w</code></mark></td><td>Writable by "Other"</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm -2</code></mark></td><td>Writable by "Other"</td></tr><tr><td><mark style="color:yellow;"><code>grep -r "w-." /</code></mark></td><td>Alternative method</td></tr></tbody></table>

Find world-writable config files:

{% code overflow="wrap" %}
```bash
find /etc -a -type f ( -name ".conf" -o -name ".cfg" -o -name "*.ini" ) -perm -o+w -exec ls -l {} ;
```
{% endcode %}

### <mark style="color:purple;">Current User</mark>

| <mark style="color:yellow;">`find / -a -writable 2>/dev/null`</mark> | Current user writable |
| -------------------------------------------------------------------- | --------------------- |
| <mark style="color:yellow;">`find / -a -perm -u+r`</mark>            | Current user writable |

Current-user writable filtering out running processes:

{% code overflow="wrap" %}
```bash
find / -a -writable 2>/dev/null | cut -d "/" -f 2,3 | grep -v proc | sort -u
```
{% endcode %}

### <mark style="color:purple;">User Specific</mark>

<table data-header-hidden><thead><tr><th width="417">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -readable</code></mark></td><td>Specific user writable</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -perm -2</code></mark></td><td>Specific user writable</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -perm -u+r</code></mark></td><td>Combines owner read permission to show files owned by user with read permissions.</td></tr></tbody></table>

### <mark style="color:purple;">Group</mark>

<table data-header-hidden><thead><tr><th width="436">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm -g+w</code></mark></td><td>Group Writable.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -group &#x3C;group_name> -readable</code></mark></td><td>Specific group Writable.</td></tr></tbody></table>

## <mark style="color:red;">Execute</mark>

### <mark style="color:purple;">Other/World</mark>

<table data-header-hidden><thead><tr><th width="280">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm -o+x</code></mark></td><td>World-executable</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm -1</code></mark></td><td>World-executable</td></tr><tr><td><mark style="color:yellow;"><code>grep -r "x-." /</code></mark></td><td>Alternative method</td></tr></tbody></table>

Finds files owned by each user where "others" have execute permission:

```bash
grep "x-" /etc/passwd | cut -d: -f1 | xargs find . -user
```

### <mark style="color:purple;">Current User</mark>

<table data-header-hidden><thead><tr><th width="284">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -executable</code></mark></td><td>Current user executable</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm -u+x</code></mark></td><td>Current user executable</td></tr></tbody></table>

### <mark style="color:purple;">User specific</mark>

<table data-header-hidden><thead><tr><th width="429">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -executable</code></mark></td><td>Specific user executable</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -perm -1</code></mark></td><td>Specific user executable</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -user [username] -perm -u+x</code></mark></td><td>Combines owner read permission to show files owned by user with read permissions</td></tr></tbody></table>

### <mark style="color:purple;">Group</mark>

<table data-header-hidden><thead><tr><th width="459">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm -g+x</code></mark></td><td>Group executable</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -group &#x3C;group_name> -executable</code></mark></td><td>Specific group executable</td></tr></tbody></table>

## <mark style="color:red;">Wide-Open</mark>

<table data-header-hidden><thead><tr><th width="294">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm 0777</code></mark></td><td>Wide open files</td></tr></tbody></table>

Find files with insecure permissions:

```bash
find / -a -type f ( -perm 777 -o -perm 666 ) -exec ls -l {} ;
```

## <mark style="color:red;">SUID/SGID</mark>

### <mark style="color:purple;">Permission Filters</mark>

`-2000` = Owner has write permissions, SGID is set. File inherits the GID of the process that executes it. `-4000` = Only files with SUID bit.\
`/6000` = SUID, SGID, or Both.

### <mark style="color:purple;">SUID Only</mark>

<table data-header-hidden><thead><tr><th width="422">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm -4000</code></mark></td><td>SUID set</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm /u=s</code></mark></td><td>SUID set</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm -4000 -user root</code></mark></td><td>SUID files owned by root</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm -4000 -not -user root</code></mark></td><td>SUID files NOT owned by root</td></tr><tr><td><mark style="color:yellow;"><code>grep -r "w-s-" /</code></mark></td><td>SUID set (Alternate method)</td></tr></tbody></table>

Processes usernames from /etc/passwd, searches for world-executable SUID files owned by each user.

{% hint style="danger" %}
Use with Caution!
{% endhint %}

```bash
grep -r "w-s-" / | cut -d: -f1 | xargs find . -user
```

### <mark style="color:purple;">SGID Only</mark>

<table data-header-hidden><thead><tr><th width="425">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm -2000</code></mark></td><td>Owner has write permissions, SGID is set</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm /u=g</code></mark></td><td>SGID set</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm -2000 -user root</code></mark></td><td>SGID set and owned by root</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm -2000 -not -user root</code></mark></td><td>SGID set and NOT owned by root</td></tr><tr><td><mark style="color:yellow;"><code>grep -r "w-S-" /</code></mark></td><td>SGID set (Alternate method)</td></tr></tbody></table>

### <mark style="color:purple;">SUID AND/OR SGID</mark>

<table data-header-hidden><thead><tr><th width="427">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -perm /6000</code></mark></td><td>SUID, SGID, or both set</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm /u=s,g=s</code></mark></td><td>Both SUID and SGID set</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm /6000 -user root</code></mark></td><td>SUID, SGID, or both set and owned by root</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm /6000 -not -user root</code></mark></td><td>SUID, SGID, or both set and NOT owned by root</td></tr></tbody></table>

SUID or SGID then execute `ls -l`:

{% code overflow="wrap" %}
```bash
find / -a \( -perm -4000 -o -perm -2000 \) -exec ls -l {} \;
```
{% endcode %}

{% code overflow="wrap" %}
```bash
find / -a -a ( -perm -u+s -o -perm -g+s ) -exec ls -l {} ; 2>/dev/null
```
{% endcode %}

## <mark style="color:red;">Capabilties</mark>

<table data-header-hidden><thead><tr><th width="399">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>getcap [filepath]</code></mark></td><td>Check a specific file for capabilities.</td></tr><tr><td><mark style="color:yellow;"><code>getcap -r [filepath]</code></mark></td><td>Recursively check capabilities of files in a directory hierarchy.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -perm -0002 | getcap -d -</code></mark></td><td>Searches for capabilities (excluding sticky bits) and pipes getcap for details.</td></tr></tbody></table>

Recursively to search for capabilities within open file descriptors, potentially revealing files in use with capabilities. Requires root privileges:

```bash
grep -r /etc/security/capabilities /proc/self/fd/*.
```

This searches for specific capabilities by name within open file descriptors of a specific process ID (PID). Requires root privileges:

```bash
grep -r "\<[CAP_>\w+]*\>" /proc/[pid]/fd/*
```
