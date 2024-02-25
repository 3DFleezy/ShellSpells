# Modify Metadata

## <mark style="color:red;">Rename</mark>

| <mark style="color:yellow;">`mv [old_name] [new_name]`</mark> | Rename                                         |
| ------------------------------------------------------------- | ---------------------------------------------- |
| <mark style="color:yellow;">`rename 's/ /_/g' *`</mark>       | Replace spaces with underscores for all files. |

## <mark style="color:red;">Timestamps</mark>

| <mark style="color:yellow;">`touch`</mark>                            | Updates <mark style="color:orange;">**access**</mark> and <mark style="color:orange;">**modification**</mark> to current datetime.   |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| <mark style="color:yellow;">`touch -t YYYYMMDDhhmm [file]`</mark>     | `-t` lets you customize the datetime. Without it, it sets to the current datetime.                                                   |
| <mark style="color:yellow;">`touch -a -t YYYYMMDDhhmm [file]`</mark>  | Updates only <mark style="color:orange;">**access**</mark> to specified datetime.                                                    |
| <mark style="color:yellow;">`touch -m -t YYYYMMDDhhmm [file]`</mark>  | Updates only <mark style="color:orange;">**modification**</mark> to specified datetime.                                              |
| <mark style="color:yellow;">`touch -d -t YYYYMMDDhhmm [file]`</mark>  | Updates <mark style="color:orange;">**access**</mark> and <mark style="color:orange;">**modification**</mark> to specific datetime.  |
| <mark style="color:yellow;">`touch -r <reference_file> [file]`</mark> | Updates <mark style="color:orange;">**access**</mark> and <mark style="color:orange;">**modification**</mark> to match another file. |

Updates \*access and \*modification of files found.

You can customize the `find` criteria to modify timestamps of specific files:

```bash
find -exec touch {} \;
```

Change the system time, which indirectly affects newly created or modified files:

```bash
date -s YYYYMMDDhhmm
```

This modifies timestamps of files listed by `ls`, extracting filenames with `awk` and using `xargs` to pipe them to `touch`:

```bash
ls -ltr | awk '{print $9}' | xargs -I {} touch -t YYYYMMDDhhmm {}
```

Note:

<mark style="color:orange;">**ctime**</mark> (change time) of a file is updated to the current system time whenever the file's metadata or content changes.

It cannot be modified directly by any command.

<mark style="color:orange;">**mtime**</mark> (modification time) is updated when the file's content changes

<mark style="color:orange;">**atime**</mark> (access time) is updated when the file's content is accessed.

## <mark style="color:red;">Ownership</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="358">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>chown [owner] [file]</code></mark></td><td>Change owner.</td></tr><tr><td><mark style="color:yellow;"><code>chown [UID] [dir]</code></mark></td><td>Change owner to UID.</td></tr><tr><td><mark style="color:yellow;"><code>chown [owner][:group] [file]</code></mark></td><td>Changes owner and/or group of a file.</td></tr><tr><td><mark style="color:yellow;"><code>chown -R [owner][:group] [dir]</code></mark></td><td>Recursively changes owner and/or group of a directory, sub-directories, and contents.</td></tr><tr><td><mark style="color:yellow;"><code>chgrp [group] [file]</code></mark></td><td>Changes group of a file to the specified group name.</td></tr><tr><td><mark style="color:yellow;"><code>chgrp 100 directory1</code></mark></td><td>Change group to GID.</td></tr><tr><td><mark style="color:yellow;"><code>chgrp -R [group] [dir]</code></mark></td><td>Recursively changes group of a directory, sub-directories, and contents.</td></tr></tbody></table>

## <mark style="color:red;">Permissions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="419">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>chmod [mode] [file]</code></mark></td><td>Changes permissions. (<mark style="color:yellow;"><code>u+x</code>, <code>g-w</code>, <code>o=r</code>) or (<code>644</code>, <code>755</code>).</mark></td></tr><tr><td><mark style="color:yellow;"><code>chmod +x [file]</code></mark></td><td>Adds execute permission for the owner, group, and others. Shorthand for <mark style="color:yellow;"><code>a+x</code> or <code>ugo+x</code>.</mark></td></tr><tr><td><mark style="color:yellow;"><code>chmod u=rwx,g=rx,o=r [file]</code></mark></td><td>Sets the permissions explicitly.</td></tr><tr><td><mark style="color:yellow;"><code>chmod 755 [file]</code></mark></td><td>Octal notation.</td></tr><tr><td><mark style="color:yellow;"><code>chmod -R mode [dir]</code></mark></td><td>Recursively changes the permissions of a directory and all its contents.</td></tr><tr><td><mark style="color:yellow;"><code>chmod --reference=&#x3C;ref_file> [file]</code></mark></td><td>Match permissions of reference file.</td></tr><tr><td><mark style="color:yellow;"><code>umask</code></mark></td><td>umask = "user file-creation mode mask". Sets the default creation permissions for new files and dirs.</td></tr><tr><td><mark style="color:yellow;"><code>umask 022</code></mark></td><td>New default permissions on created files and dirs is 755.</td></tr></tbody></table>

Note:

<mark style="color:yellow;">4</mark> = read (<mark style="color:yellow;">`r`</mark><mark style="color:yellow;">)</mark>

<mark style="color:yellow;">2</mark> = write (<mark style="color:yellow;">`w`</mark><mark style="color:yellow;">)</mark>

<mark style="color:yellow;">1</mark> = execute (<mark style="color:yellow;">`x`</mark><mark style="color:yellow;">)</mark>

<mark style="color:yellow;">`+`</mark> (add permission)

<mark style="color:yellow;">`-`</mark> (remove permission)

<mark style="color:yellow;">`=`</mark> (set permission exactly)

## <mark style="color:red;">Attributes</mark>

| <mark style="color:yellow;">`chattr [+,-,=][attributes] [file]`</mark> | Modify attributes                             |
| ---------------------------------------------------------------------- | --------------------------------------------- |
| <mark style="color:yellow;">`chattr =i [file]`</mark>                  | Make file immutable, clears other attributes. |

<mark style="color:yellow;">`a`</mark> (Append only): Can be added to, but existing data cannot be modified or deleted. This is useful for log files.

<mark style="color:yellow;">`i`</mark> (Immutable): Cannot be modified: it cannot be deleted, renamed, or linked, and no data can be written to it. Only the root user can set or clear this attribute.

<mark style="color:yellow;">`s`</mark> (Secure deletion): When a file with this attribute is deleted, its data is immediately overwritten with zeros. This makes recovering the file's data more difficult.

<mark style="color:yellow;">`S`</mark> (Synchronous update): This attribute ensures that modifications to the file are written synchronously to the disk, similar to how the `sync` command works.

<mark style="color:yellow;">`A`</mark> (No atime updates): Normally, the access time of a file is updated whenever it's read. Setting this attribute stops those updates, which can improve performance for certain applications.

## <mark style="color:red;">Capabilities</mark>

<table data-header-hidden><thead><tr><th width="432">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>setcap [capabilities] [file]</code></mark></td><td>Set capabilities</td></tr><tr><td><mark style="color:yellow;"><code>setcap 'cap_net_bind_service+ep' [file]</code></mark></td><td>Set capability as <mark style="color:yellow;"><code>e</code>-effectivce and <code>p</code>-permitted</mark></td></tr></tbody></table>

### <mark style="color:purple;">Operators and Sets</mark>

<mark style="color:yellow;">`+`</mark> (Add)

<mark style="color:yellow;">`-`</mark> (Remove)

<mark style="color:yellow;">`=`</mark> (Set): Explicitly sets capabilities, replacing any existing capabilities.

<mark style="color:orange;">**Effective**</mark> (`e`): Which capabilities are "active" and can be used by the process.

<mark style="color:orange;">**Permitted**</mark> (`p`): Which capabilities the process can use or gain. If a capability is in the permitted set, it can be added to the effective set by the process.

<mark style="color:orange;">**Inheritable**</mark> (`i`): This set determines which capabilities can be inherited by child processes. If a capability is in the inheritable set of a parent process and also in the permitted set of an executable being run by that process, it can be added to the permitted and effective sets of the child process.<==

### <mark style="color:purple;">Capability Options</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="220">Capability</th><th>Description</th></tr></thead><tbody><tr><td>cap_chown</td><td>Allows changing the owner of any file.</td></tr><tr><td>cap_dac_override</td><td>Bypasses file read, write, and execute permission checks.</td></tr><tr><td>cap_dac_read_search</td><td>Bypasses file read permission checks and directory read and execute permission checks.</td></tr><tr><td>cap_fowner</td><td>Bypasses permission checks on operations that normally require the filesystem UID of the process to match the UID of the file (e.g., chown, chmod).</td></tr><tr><td>cap_fsetid</td><td>Allows setting the set-user-ID and set-group-ID bits on files; allows setgid to work on a file regardless of the file's GID.</td></tr><tr><td>cap_kill</td><td>Allows sending signals to any process, bypassing permission checks.</td></tr><tr><td>cap_net_bind_service</td><td>Allows binding to TCP/UDP sockets below 1024, which are normally reserved for processes with root privileges.</td></tr><tr><td>cap_net_broadcast</td><td>Allows sending broadcast packets over a network.</td></tr><tr><td>cap_net_admin</td><td>Allows various network-related operations, such as interface configuration, administration of IP firewall, masquerading, and routing.</td></tr><tr><td>cap_net_raw</td><td>Allows using RAW and PACKET sockets, providing the capability to craft packets that could manipulate the network, which is potentially dangerous.</td></tr><tr><td>cap_ipc_lock</td><td>Allows locking memory segments, preventing them from being swapped out to disk.</td></tr><tr><td>cap_ipc_owner</td><td>Bypasses permission checks for operations on System V IPC objects.</td></tr><tr><td>cap_sys_module</td><td>Allows loading and unloading kernel modules.</td></tr><tr><td>cap_sys_rawio</td><td>Allows direct I/O access to hardware devices.</td></tr><tr><td>cap_sys_chroot</td><td>Allows using the chroot() system call, changing the root directory of a process.</td></tr><tr><td>cap_sys_ptrace</td><td>Allows using ptrace(), useful for debugging and tracing system calls.</td></tr><tr><td>cap_sys_pacct</td><td>Allows managing process accounting files.</td></tr><tr><td>cap_sys_admin</td><td>A broad capability allowing various system administration operations, like mounting filesystems, configuring the kernel, and more.</td></tr><tr><td>cap_sys_boot</td><td>Allows rebooting or enabling/disabling device power.</td></tr><tr><td>cap_sys_nice</td><td>Allows raising process priorities and setting real-time scheduling policies.</td></tr><tr><td>cap_sys_resource</td><td>Allows overriding resource limits.</td></tr><tr><td>cap_sys_time</td><td>Allows setting the system clock.</td></tr><tr><td>cap_sys_tty_config</td><td>Allows configuration of tty devices.</td></tr><tr><td>cap_mknod</td><td>Allows creation of special files using mknod().</td></tr><tr><td>cap_lease</td><td>Allows establishing leases on arbitrary files (useful for locking).</td></tr><tr><td>cap_audit_write</td><td>Allows writing to the kernel audit log.</td></tr><tr><td>cap_audit_control</td><td>Allows control over kernel audit system.</td></tr><tr><td>cap_setfcap</td><td>Allows setting file capabilities.</td></tr></tbody></table>

## <mark style="color:red;">Links</mark>

| Command                                                                             | Description |
| ----------------------------------------------------------------------------------- | ----------- |
| <mark style="color:yellow;">`ln <source_file> <target_file>`</mark>                 | Hard link   |
| <mark style="color:yellow;">`ln -s <source_file> <target_file>`</mark>===> \*\*\*\* | Soft link   |

### <mark style="color:purple;">Hard links</mark>

Useful for saving disk space as they share the same data

Deleting one removes the data if it's the last link.

They cannot link across filesystems or to directories.

### <mark style="color:purple;">Soft links</mark>

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
