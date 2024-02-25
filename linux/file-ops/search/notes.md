# Notes

## Grep Command

```bash
grep -IRil "pattern" /path/to/search
```

<mark style="color:yellow;">`-I`</mark> Ignore binaries (.bin, .jpg, etc)\
<mark style="color:yellow;">`-R`</mark> Recursive + follows all symlinks\
<mark style="color:yellow;">`-i`</mark> Case-insensitive\
<mark style="color:yellow;">`-l`</mark> Shows only filenames with pattern in the content

### `-r` vs. `-R`

<mark style="color:yellow;">`-r`</mark>  Follows symbolic links by default. It searches through the contents of symbolic links if they point to directories, effectively treating them as directories.

<mark style="color:yellow;">`-R`</mark> Does not follow symbolic links. It treats symbolic links as regular files and does not search through their contents.

<mark style="color:yellow;">`grep -r [pattern] .`</mark> Will <mark style="color:orange;">**NOT**</mark> follow the symlinks\
<mark style="color:yellow;">`grep -R [pattern] .`</mark> Will <mark style="color:orange;">**NOT**</mark> follow the symlinks\
<mark style="color:yellow;">`grep -r [pattern] *`</mark> <mark style="color:orange;">**WILL**</mark> follow symlinks



## Locate Command&#x20;

Remember that <mark style="color:yellow;">`locate`</mark> relies on the <mark style="color:yellow;">`updatedb`</mark> to be up-to-date.



## Find Command

<mark style="color:yellow;">`find . -print`</mark> will print only filenames without additional info. \
The <mark style="color:yellow;">`-depth`</mark> option changes the order in which directories are searched. \
By default, find traverses the entire directory tree before returning any results. \
With <mark style="color:yellow;">`-depth`</mark>, it processes each directory and its contents immediately after finding it.

You can disable recursion using the <mark style="color:yellow;">`-maxdepth <depth>`</mark> option\
<mark style="color:yellow;">`find . -maxdepth 1`</mark>

<mark style="color:yellow;">`-exec`</mark>\
<mark style="color:yellow;">`{}`</mark>= filename placeholder for <mark style="color:yellow;">`exec`</mark>\
<mark style="color:yellow;">`\;`</mark>= escaped command terminator for <mark style="color:yellow;">`exec`</mark>



