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
| <mark style="color:yellow;">`namei /sbin/init`</mark>         | Shows available links to the file. D = dir, F = File, L = Link  |
| <mark style="color:yellow;">`namei -mo /sbin/init`</mark>     | Better, shows file permissions and owners                       |

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



## <mark style="color:red;">Permission Notes</mark>

```bash
+------------------------+
| Owner	| Group | Others |
| R W E	| R W E | R W E	 |
| 4 2 1	| 4 2 1 | 4 2 1	 |
+------------------------+
```

SUID (4): \
Execute with owner's permissions.

SGID (2):\
Execute with owning group's permissions.

Sticky Bit (1): \
Can't delete these files. Often root owned dirs. Only for dirs.



### <mark style="color:purple;">Necessary Permissions by Action</mark>

```bash
Actions			    Dir	    File
----------------------------------------
Read File		    X	    R
Modify File		    X	    W
Create File		    WX	
Delete File		    WX	
Move File		    WX	    WX
Dir Listing		    R	
Dir Listing w/ Metadata	    RX
Execute Binary		    X	    X
Execute Script		    X	    RX
```



## <mark style="color:red;">Timestamp Notes</mark>

<mark style="color:orange;">ctime</mark> = Inode change

<mark style="color:orange;">mtime</mark> = Content change

<mark style="color:orange;">atime</mark> = Access time

<mark style="color:yellow;">`stat`</mark> - View inode info and timestamps of a file

Inode: Metadata about a file. Has pointers to the data that the file holds. Keeps track of file meteadata.&#x20;

Changing the owner of a file changes <mark style="color:orange;">`ctime`</mark> Creating a file changes ctime

Anytime the content is changed, the <mark style="color:orange;">`ctime`</mark> is also changed, because the size of the file changes

Anytime file is moved or copied the path changes so the <mark style="color:orange;">`ctime`</mark> also changes.

Anytime file is opened or executed, <mark style="color:orange;">`atime`</mark> is changed.



#### <mark style="color:green;">Testing:</mark>



If you...

Create a dir

Go in to that dir

Create a subdir

Run stat on the original dir

The <mark style="color:orange;">`atime`</mark> and <mark style="color:orange;">`ctime`</mark> does NOT change.



If you...

Create a dir

Do NOT go in to that dir

Create a subdir

Run stat on the original dir

ALL times change. Except <mark style="color:orange;">`birth`</mark> time.



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
