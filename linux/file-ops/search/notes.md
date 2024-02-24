# Notes

## Grep Command

`grep -IRil "pattern" /path/to/search`

`-I` Ignore binaries (.bin, .jpg, etc)\
`-R` Recursive + follows all symlinks\
`-i` Case-insensitive\
`-l` Shows only filenames with pattern in the content

### `-r` vs. `-R`

`-r`  Follows symbolic links by default. It searches through the contents of symbolic links if they point to directories, effectively treating them as directories.

`-R` Does not follow symbolic links. It treats symbolic links as regular files and does not search through their contents.

`grep -r [pattern] .` Will <mark style="color:orange;">**NOT**</mark> follow the symlinks\
`grep -R [pattern] .` Will <mark style="color:orange;">**NOT**</mark> follow the symlinks\
`grep -r [pattern] *` <mark style="color:orange;">**WILL**</mark> follow symlinks



## Locate Command&#x20;

Remember that `locate` relies on the `updatedb` to be up-to-date.



## Find Command

`find . -print` will print only filenames without additional info. \
The `-depth` option changes the order in which directories are searched. \
By default, find traverses the entire directory tree before returning any results. \
With `-depth`, it processes each directory and its contents immediately after finding it.

You can disable recursion using the `-maxdepth <depth>` option\
`find . -maxdepth 1`

`-exec`\
`{}`= filename placeholder for `exec`\
`\;`= escaped command terminator for `exec`



