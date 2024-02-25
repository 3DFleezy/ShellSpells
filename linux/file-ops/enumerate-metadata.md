# Enumerate Metadata

## <mark style="color:red;">Commands</mark>

| <mark style="color:yellow;">`ls -lisa`</mark>                 | File info                                                       |
| ------------------------------------------------------------- | --------------------------------------------------------------- |
| <mark style="color:yellow;">`file [file]`</mark>              | Determine File Type.                                            |
| <mark style="color:yellow;">`stat [file]`</mark>              | Display Detailed File Information.                              |
| <mark style="color:yellow;">`statvfs [directory_path]`</mark> | Display Filesystem Information.                                 |
| <mark style="color:yellow;">`lsattr [filename]`</mark>        | Lists the attributes of the specified file.                     |
| <mark style="color:yellow;">`getfacl [filename]`</mark>       | Displays the Access Control Lists (ACLs) of the specified file. |
| <mark style="color:yellow;">`getcap [filepath]`</mark>        | Check a specific file for capabilities                          |
| <mark style="color:yellow;">`getcap -r [filepath]`</mark>     | Recursive                                                       |

### <mark style="color:purple;">Identifying Symlinks and Hard Links</mark>

<mark style="color:yellow;">`ls -l`</mark>

Look at the third column:

Hard link: The number in this column represents the number of hard links pointing to the same data block. If it's greater than 1, it's a hard link.

Soft link: This column will display a hyphen (-) followed by the file size and filename of the file the link points to.

<mark style="color:yellow;">`file`</mark>

The output will tell you the file type.

Hard link: It will say something like "inode link to "

Soft link: It will say "symbolic link to "

<mark style="color:yellow;">`stat`</mark>

Look for the following differences:

Hard link: st\_ino (inode number) will be the same for both the link and the original file.

Soft link: st\_ino will be different for the link and the original file.

## <mark style="color:red;">ls Options</mark>

<mark style="color:yellow;">`-a`</mark> or <mark style="color:yellow;">`--all`</mark>

<mark style="color:yellow;">`-l`</mark> or <mark style="color:yellow;">`--long`</mark>

<mark style="color:yellow;">`-h`</mark> or <mark style="color:yellow;">`--human-readable`</mark>

<mark style="color:yellow;">`-R`</mark> or <mark style="color:yellow;">`--recursive`</mark>

<mark style="color:yellow;">`-t`</mark> or <mark style="color:yellow;">`--sort=time`</mark>

<mark style="color:yellow;">`-S`</mark> or <mark style="color:yellow;">`--sort=size`</mark>

<mark style="color:yellow;">`-r`</mark> or <mark style="color:yellow;">`--reverse`</mark>

<mark style="color:yellow;">`-i`</mark> or <mark style="color:yellow;">`--inode`</mark>

<mark style="color:yellow;">`-d`</mark> or <mark style="color:yellow;">`--directory`</mark>

<mark style="color:yellow;">`-g`</mark> or <mark style="color:yellow;">`--group`</mark>

<mark style="color:yellow;">`-o`</mark> or <mark style="color:yellow;">`--owner`</mark>

<mark style="color:yellow;">`-F`</mark> or <mark style="color:yellow;">`--classify`</mark>

<mark style="color:yellow;">`-p`</mark> or <mark style="color:yellow;">`--indicator-style=slash`</mark>

<mark style="color:yellow;">`--color`</mark>

<mark style="color:yellow;">`-c`</mark> or <mark style="color:yellow;">`--time=ctime`</mark>

<mark style="color:yellow;">`-u`</mark> or <mark style="color:yellow;">`--time=atime`</mark>

<mark style="color:yellow;">`-1`</mark> or <mark style="color:yellow;">`--format=single-column`</mark>

<mark style="color:yellow;">`--group-directories-first`</mark>
