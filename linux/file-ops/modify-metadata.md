# Modify Metadata

## Rename

| Command                    | Description                                    |
| -------------------------- | ---------------------------------------------- |
| `mv [old_name] [new_name]` | Rename                                         |
| `rename 's/ /_/g' *`       | Replace spaces with underscores for all files. |



## Timestamps

| Command                            | Description                                                                        |
| ---------------------------------- | ---------------------------------------------------------------------------------- |
| `touch`                            | Updates access and modification to current datetime.                               |
| `touch -t YYYYMMDDhhmm [file]`     | `-t` lets you customize the datetime. Without it, it sets to the current datetime. |
| `touch -a -t YYYYMMDDhhmm [file]`  | Updates only \*access to specified datetime.                                       |
| `touch -m -t YYYYMMDDhhmm [file]`  | Updates only \*modification to specified datetime.                                 |
| `touch -d -t YYYYMMDDhhmm [file]`  | Updates \*access and \*modification to specific datetime.                          |
| `touch -r <reference_file> [file]` | Updates \*access and \*modification to match another file.                         |

Updates \*access and \*modification of files found.

You can customize the `find` criteria to modify timestamps of specific files:

`find -exec touch {} \;`

Change the system time, which indirectly affects newly created or modified files:

`date -s YYYYMMDDhhmm`

This modifies timestamps of files listed by `ls`, extracting filenames with `awk` and using `xargs` to pipe them to `touch`:

`ls -ltr | awk '{print $9}' | xargs -I {} touch -t YYYYMMDDhhmm {}`

Note:

\*ctime (change time) of a file is updated to the current system time whenever the file's metadata or content changes.

It cannot be modified directly by any command.

\*mtime (modification time) is updated when the file's content changes

\*atime (access time) is updated when the file's content is accessed.



## Ownership

| Command                          | Description                                                                           |
| -------------------------------- | ------------------------------------------------------------------------------------- |
| `chown [owner] [file]`           | Change owner.                                                                         |
| `chown [UID] [dir]`              | Change owner to UID.                                                                  |
| `chown [owner][:group] [file]`   | Changes owner and/or group of a file.                                                 |
| `chown -R [owner][:group] [dir]` | Recursively changes owner and/or group of a directory, sub-directories, and contents. |
| `chgrp [group] [file]`           | Changes group of a file to the specified group name.                                  |
| `chgrp 100 directory1`           | Change group to GID.                                                                  |
| `chgrp -R [group] [dir]`         | Recursively changes group of a directory, sub-directories, and contents.              |



## Permissions

| Command                               | Description                                                                                           |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `chmod [mode] [file]`                 | Changes permissions. (`u+x`, `g-w`, `o=r`) or (`644`, `755`).                                         |
| `chmod +x [file]`                     | Adds execute permission for the owner, group, and others. Shorthand for `a+x` or `ugo+x`.             |
| `chmod u=rwx,g=rx,o=r [file]`         | Sets the permissions explicitly.                                                                      |
| `chmod 755 [file]`                    | Octal notation.                                                                                       |
| `chmod -R mode [dir]`                 | Recursively changes the permissions of a directory and all its contents.                              |
| `chmod --reference=<ref_file> [file]` | Match permissions of reference file.                                                                  |
| `umask`                               | umask = "user file-creation mode mask". Sets the default creation permissions for new files and dirs. |
| `umask 022`                           | New default permissions on created files and dirs is 755.                                             |

Note:

4 = read (`r`)

2 = write (`w`)

1 = execute (`x`)

`+` (add permission)

`-` (remove permission)

`=` (set permission exactly)



## Attributes

| Command                             | Description                                   |
| ----------------------------------- | --------------------------------------------- |
| `chattr [+,-,=][attributes] [file]` | Modify attributes                             |
| `chattr =i [file]`                  | Make file immutable, clears other attributes. |

Attributes:

`a` (Append only): Can be added to, but existing data cannot be modified or deleted. This is useful for log files.

`i` (Immutable): Cannot be modified: it cannot be deleted, renamed, or linked, and no data can be written to it. Only the root user can set or clear this attribute.

`s` (Secure deletion): When a file with this attribute is deleted, its data is immediately overwritten with zeros. This makes recovering the file's data more difficult.

`S` (Synchronous update): This attribute ensures that modifications to the file are written synchronously to the disk, similar to how the `sync` command works.

`A` (No atime updates): Normally, the access time of a file is updated whenever it's read. Setting this attribute stops those updates, which can improve performance for certain applications.



## Capabilities

| Command                                   | Description                                        |
| ----------------------------------------- | -------------------------------------------------- |
| `setcap [capabilities] [file]`            | Set capabilities                                   |
| `setcap 'cap_net_bind_service+ep' [file]` | Set capability as `e`-effectivce and `p`-permitted |

### Operators and Sets

`+` (Add)

`-` (Remove)

`=` (Set): Explicitly sets capabilities, replacing any existing capabilities.

<mark style="color:orange;">**Effective**</mark> (`e`): Which capabilities are "active" and can be used by the process.

<mark style="color:orange;">**Permitted**</mark> (`p`): Which capabilities the process can use or gain. If a capability is in the permitted set, it can be added to the effective set by the process.

<mark style="color:orange;">**Inheritable**</mark> (`i`): This set determines which capabilities can be inherited by child processes. If a capability is in the inheritable set of a parent process and also in the permitted set of an executable being run by that process, it can be added to the permitted and effective sets of the child process.<==

### Capability Options

| Capability              | Description                                                                                                                                         |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| cap\_chown              | Allows changing the owner of any file.                                                                                                              |
| cap\_dac\_override      | Bypasses file read, write, and execute permission checks.                                                                                           |
| cap\_dac\_read\_search  | Bypasses file read permission checks and directory read and execute permission checks.                                                              |
| cap\_fowner             | Bypasses permission checks on operations that normally require the filesystem UID of the process to match the UID of the file (e.g., chown, chmod). |
| cap\_fsetid             | Allows setting the set-user-ID and set-group-ID bits on files; allows setgid to work on a file regardless of the file's GID.                        |
| cap\_kill               | Allows sending signals to any process, bypassing permission checks.                                                                                 |
| cap\_net\_bind\_service | Allows binding to TCP/UDP sockets below 1024, which are normally reserved for processes with root privileges.                                       |
| cap\_net\_broadcast     | Allows sending broadcast packets over a network.                                                                                                    |
| cap\_net\_admin         | Allows various network-related operations, such as interface configuration, administration of IP firewall, masquerading, and routing.               |
| cap\_net\_raw           | Allows using RAW and PACKET sockets, providing the capability to craft packets that could manipulate the network, which is potentially dangerous.   |
| cap\_ipc\_lock          | Allows locking memory segments, preventing them from being swapped out to disk.                                                                     |
| cap\_ipc\_owner         | Bypasses permission checks for operations on System V IPC objects.                                                                                  |
| cap\_sys\_module        | Allows loading and unloading kernel modules.                                                                                                        |
| cap\_sys\_rawio         | Allows direct I/O access to hardware devices.                                                                                                       |
| cap\_sys\_chroot        | Allows using the chroot() system call, changing the root directory of a process.                                                                    |
| cap\_sys\_ptrace        | Allows using ptrace(), useful for debugging and tracing system calls.                                                                               |
| cap\_sys\_pacct         | Allows managing process accounting files.                                                                                                           |
| cap\_sys\_admin         | A broad capability allowing various system administration operations, like mounting filesystems, configuring the kernel, and more.                  |
| cap\_sys\_boot          | Allows rebooting or enabling/disabling device power.                                                                                                |
| cap\_sys\_nice          | Allows raising process priorities and setting real-time scheduling policies.                                                                        |
| cap\_sys\_resource      | Allows overriding resource limits.                                                                                                                  |
| cap\_sys\_time          | Allows setting the system clock.                                                                                                                    |
| cap\_sys\_tty\_config   | Allows configuration of tty devices.                                                                                                                |
| cap\_mknod              | Allows creation of special files using mknod().                                                                                                     |
| cap\_lease              | Allows establishing leases on arbitrary files (useful for locking).                                                                                 |
| cap\_audit\_write       | Allows writing to the kernel audit log.                                                                                                             |
| cap\_audit\_control     | Allows control over kernel audit system.                                                                                                            |
| cap\_setfcap            | Allows setting file capabilities.                                                                                                                   |



## Links

| Command                             | Description |
| ----------------------------------- | ----------- |
| `ln <source_file> <target_file>`    | Hard link   |
| `ln -s <source_file> <target_file>` | Soft link   |

### Hard links

Useful for saving disk space as they share the same data

Deleting one removes the data if it's the last link.

They cannot link across filesystems or to directories.

### Soft links

Handy for creating flexible shortcuts that work across filesystems and can point to directories.

The original file needs to exist for the link to work

Deleting the original file breaks the link.

#### <mark style="color:green;">Choosing the Right Option</mark>

Use hard links when you want to save disk space and ensure multiple "names" access the same data. But be cautious about deleting links.

Use soft links for flexible shortcuts across filesystems or to directories, but remember they rely on the original file existing.

#### <mark style="color:green;">Key Differences</mark>

| Attributes           | Hard Link                       | Soft Link (Symbolic Link)                                                      |
| -------------------- | ------------------------------- | ------------------------------------------------------------------------------ |
| Data                 | Location                        | Same as original file, separate file, stores path                              |
| Size                 | Same as original file           | Small (contains path only)                                                     |
| Number of Links      | Multiple possible               | Only one per original file                                                     |
| Works across FS      | No                              | Yes                                                                            |
| Links to directories | Not possible                    | Yes                                                                            |
| Deletion impact      | Deleting last link removes data | Deleting link doesn't affect original file, deleting original file breaks link |
