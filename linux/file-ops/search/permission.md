# Permission

## Read

### Other/World

| Command                | Description        |
| ---------------------- | ------------------ |
| `find / -a -perm -o+r` | World-readable     |
| `find / -a -perm -4`   | World-readable     |
| `grep -r "r-." /`      | Alternative method |

Extracts usernames from /etc/passwd and finds files owned by each user where "others" have read permission (Need to test):

```bash
grep "r-" /etc/passwd | cut -d: -f1 | xargs find . -user
```

### Current User

| Command                | Description            |
| ---------------------- | ---------------------- |
| `find / -a -readable`  | Current user readable. |
| `find / -a -perm -u+r` | Current user readable. |

### User specific

| Command                                 | Description                                                                       |
| --------------------------------------- | --------------------------------------------------------------------------------- |
| `find / -a -user [username] -readable`  | Specific user readable.                                                           |
| `find / -a -user [username] -perm -4`   | Specific user readable.                                                           |
| `find / -a -user [username] -perm -u+r` | Combines owner read permission to show files owned by user with read permissions. |

### Group

| Command                                   | Description              |
| ----------------------------------------- | ------------------------ |
| `find / -a -perm -g+r`                    | Group readable.          |
| `find / -a -group <group_name> -readable` | Specific group readable. |

## Write

### Other/World

| Command                | Description         |
| ---------------------- | ------------------- |
| `find / -a -perm -o+w` | Writable by "Other" |
| `find / -a -perm -2`   | Writable by "Other" |
| `grep -r "w-." /`      | Alternative method  |

Find world-writable config files:

{% code overflow="wrap" %}
```bash
find /etc -a -type f ( -name ".conf" -o -name ".cfg" -o -name "*.ini" ) -perm -o+w -exec ls -l {} ;
```
{% endcode %}

### Current User

| Command                           | Description           |
| --------------------------------- | --------------------- |
| `find / -a -writable 2>/dev/null` | Current user writable |
| `find / -a -perm -u+r`            | Current user writable |

Current-user writable filtering out running processes:

{% code overflow="wrap" %}
```bash
find / -a -writable 2>/dev/null | cut -d "/" -f 2,3 | grep -v proc | sort -u
```
{% endcode %}

### User Specific

| Command                                 | Description                                                                       |
| --------------------------------------- | --------------------------------------------------------------------------------- |
| `find / -a -user [username] -readable`  | Specific user writable                                                            |
| `find / -a -user [username] -perm -2`   | Specific user writable                                                            |
| `find / -a -user [username] -perm -u+r` | Combines owner read permission to show files owned by user with read permissions. |

### Group

| Command                                   | Description              |
| ----------------------------------------- | ------------------------ |
| `find / -a -perm -g+w`                    | Group Writable.          |
| `find / -a -group <group_name> -readable` | Specific group Writable. |

## Execute

### Other/World

| Command                | Description        |
| ---------------------- | ------------------ |
| `find / -a -perm -o+x` | World-executable   |
| `find / -a -perm -1`   | World-executable   |
| `grep -r "x-." /`      | Alternative method |

Finds files owned by each user where "others" have execute permission:

```bash
grep "x-" /etc/passwd | cut -d: -f1 | xargs find . -user
```

### Current User

| Command                 | Description             |
| ----------------------- | ----------------------- |
| `find / -a -executable` | Current user executable |
| `find / -a -perm -u+x`  | Current user executable |

### User specific

| Command                                  | Description                                                                      |
| ---------------------------------------- | -------------------------------------------------------------------------------- |
| `find / -a -user [username] -executable` | Specific user executable                                                         |
| `find / -a -user [username] -perm -1`    | Specific user executable                                                         |
| `find / -a -user [username] -perm -u+x`  | Combines owner read permission to show files owned by user with read permissions |

### Group

| Command                                     | Description               |
| ------------------------------------------- | ------------------------- |
| `find / -a -perm -g+x`                      | Group executable          |
| `find / -a -group <group_name> -executable` | Specific group executable |

## Wide-Open

| Command                | Description     |
| ---------------------- | --------------- |
| `find / -a -perm 0777` | Wide open files |

Find files with insecure permissions:

```bash
find / -a -type f ( -perm 777 -o -perm 666 ) -exec ls -l {} ;
```

## SUID/SGID

### Permission Filters

`-2000` = Owner has write permissions, SGID is set. File inherits the GID of the process that executes it. `-4000` = Only files with SUID bit. \
`/6000` = SUID, SGID, or Both.

### SUID Only

| Command                                 | Description                  |
| --------------------------------------- | ---------------------------- |
| `find / -a -perm -4000`                 | SUID set                     |
| `find / -a -perm /u=s`                  | SUID set                     |
| `find / -a -perm -4000 -user root`      | SUID files owned by root     |
| `find / -a -perm -4000 -not -user root` | SUID files NOT owned by root |
| `grep -r "w-s-" /`                      | SUID set (Alternate method)  |

Processes usernames from /etc/passwd, searches for world-executable SUID files owned by each user.&#x20;

{% hint style="danger" %}
Use with Caution!
{% endhint %}

```bash
grep -r "w-s-" / | cut -d: -f1 | xargs find . -user
```

### SGID Only

| Command                                 | Description                              |
| --------------------------------------- | ---------------------------------------- |
| `find / -a -perm -2000`                 | Owner has write permissions, SGID is set |
| `find / -a -perm /u=g`                  | SGID set                                 |
| `find / -a -perm -2000 -user root`      | SGID set and owned by root               |
| `find / -a -perm -2000 -not -user root` | SGID set and NOT owned by root           |
| `grep -r "w-S-" /`                      | SGID set (Alternate method)              |

### SUID AND/OR SGID

| Command                                 | Description                                   |
| --------------------------------------- | --------------------------------------------- |
| `find / -a -perm /6000`                 | SUID, SGID, or both set                       |
| `find / -a -perm /u=s,g=s`              | Both SUID and SGID set                        |
| `find / -a -perm /6000 -user root`      | SUID, SGID, or both set and owned by root     |
| `find / -a -perm /6000 -not -user root` | SUID, SGID, or both set and NOT owned by root |

SUID or SGID then execute `ls -l`: &#x20;

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

## Capabilties

| Command                                | Description                                                                     |
| -------------------------------------- | ------------------------------------------------------------------------------- |
| `getcap [filepath]`                    | Check a specific file for capabilities.                                         |
| `getcap -r [filepath]`                 | Recursively check capabilities of files in a directory hierarchy.               |
| `find / -a -perm -0002 \| getcap -d -` | Searches for capabilities (excluding sticky bits) and pipes getcap for details. |

Recursively to search for capabilities within open file descriptors, potentially revealing files in use with capabilities. Requires root privileges:

```bash
grep -r /etc/security/capabilities /proc/self/fd/*.
```

This searches for specific capabilities by name within open file descriptors of a specific process ID (PID). Requires root privileges:

```bash
grep -r "\<[CAP_>\w+]*\>" /proc/[pid]/fd/*
```
