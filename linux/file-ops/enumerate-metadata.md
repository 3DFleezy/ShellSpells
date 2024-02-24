# Enumerate Metadata

## Commands

| Command                    | Description                                                     |
| -------------------------- | --------------------------------------------------------------- |
| `ls -lisa`                 | File info                                                       |
| `file [file]`              | Determine File Type.                                            |
| `stat [file]`              | Display Detailed File Information.                              |
| `statvfs [directory_path]` | Display Filesystem Information.                                 |
| `lsattr [filename]`        | Lists the attributes of the specified file.                     |
| `getfacl [filename]`       | Displays the Access Control Lists (ACLs) of the specified file. |
| `getcap [filepath]`        | Check a specific file for capabilities                          |
| `getcap -r [filepath]`     | Recursive                                                       |



### Identifying Symlinks and Hard Links

`ls -l`

Look at the third column:

Hard link: The number in this column represents the number of hard links pointing to the same data block. If it's greater than 1, it's a hard link.

Soft link: This column will display a hyphen (-) followed by the file size and filename of the file the link points to.

`file`

The output will tell you the file type.

Hard link: It will say something like "inode link to "

Soft link: It will say "symbolic link to "

`stat`

Look for the following differences:

Hard link: st\_ino (inode number) will be the same for both the link and the original file.

Soft link: st\_ino will be different for the link and the original file.



## ls Options

`-a` or `--all`

`-l` or `--long`

`-h` or `--human-readable`

`-R` or `--recursive`

`-t` or `--sort=time`

`-S` or `--sort=size`

`-r` or `--reverse`

`-i` or `--inode`

`-d` or `--directory`

`-g` or `--group`

`-o` or `--owner`

`-F` or `--classify`

`-p` or `--indicator-style=slash`

`--color`&#x20;

`-c` or `--time=ctime`

`-u` or `--time=atime`

`-1` or `--format=single-column`

`--group-directories-first`
