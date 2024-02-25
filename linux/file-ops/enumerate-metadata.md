# Enumerate Metadata

## <mark style="color:red;">Commands</mark>

| Command | Description |
| -------------------------- | --------------------------------------------------------------- |
| <mark style="color:yellow;">`ls -lisa`</mark>                 | File info                                                       |
| <mark style="color:yellow;">`file [file]`</mark>              | Determine File Type.                                            |
| <mark style="color:yellow;">`stat [file]`</mark>              | Display Detailed File Information.                              |
| <mark style="color:yellow;">`statvfs [directory_path]`</mark> | Display Filesystem Information.                                 |
| <mark style="color:yellow;">`lsattr [filename]`</mark>        | Lists the attributes of the specified file.                     |
| <mark style="color:yellow;">`getfacl [filename]`</mark>       | Displays the Access Control Lists (ACLs) of the specified file. |
| <mark style="color:yellow;">`getcap [filepath]`</mark>        | Check a specific file for capabilities                          |
| <mark style="color:yellow;">`getcap -r [filepath]`</mark>     | Recursive                                                       |



### <mark style="color:purple;">Identifying Symlinks and Hard Links</mark>

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



## <mark style="color:red;">ls Options</mark>

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
