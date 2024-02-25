# Filename

## <mark style="color:red;">Filenames</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="420">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>grep -rli file*</code></td><td>Pattern match</td></tr><tr><td><mark style="color:yellow;"><code>grep -rli "filename" /path/to/search</code></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>ls -R [directory] | grep "filename"</code></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -iname "filename"</code></td><td>Case insensitive</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name password.txt</code></td><td>Recursive exact match</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -name "pat*tern"</code></td><td>Pattern match "pat" and ending with "tern"</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type d -name config</code></td><td>Exact directory match</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type d -name "\*687-250\*"</code></td><td>Pattern directory match</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -regex "regex_pattern"</code></td><td>Regex</td></tr><tr><td><mark style="color:yellow;"><code>locate "[filename]"</code></td><td>Uses a database updated by <mark style="color:yellow;"><code>updatedb</code> to quickly locate files</td></tr><tr><td><mark style="color:yellow;"><code>locate -i "[filename]"</code></td><td>Case-insensitive</td></tr></tbody></table>

Use extended regex syntax:

```bash
find / -a -regextype egrep -regex "pat.+?ern"
```

Use Perl regex syntax:

```bash
find / -a -regextype perl -regex "^user_[0-9]+.sh$"
```

Uses `xargs` for efficiency with a large number of files

```bash
find / -a -type f -print0 | xargs -0 grep -l "[string]"
```

Finds files by name and then executes `ls -lh`:

```bash
find / -a -type f -name "[filename]" -exec ls -lh {} +
```

Find development tools and supported languages:

```bash
find / -a -name perl*
find / -a -name python*
find / -a -name gcc*
```



## <mark style="color:red;">File Extensions</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="572">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ls [directory]/*.ext</code></td><td>Not Recursive</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f \( -name "*.txt" -o -name "*.sh" \)</code></td><td>Multiple file extensions.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name "*.txt"</code></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -iname "*.txt"</code></td><td>Case-insensitive.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -regex ".*\.txt"</code></td><td>Use regular expressions.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -regextype posix -regex ".+\.log$"</code></td><td>Matches all files ending with .log, using POSIX regex syntax.</td></tr><tr><td><mark style="color:yellow;"><code>grep -rli "\.txt$" /path/to/search</code></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>grep -rli --include=\*.ext "pattern" [directory]</code></td><td>Recursively searches for files with the <mark style="color:yellow;"><code>.ext</code> extension containing "pattern" in the specified directory.</td></tr></tbody></table>



## <mark style="color:red;">Search Multiple Dirs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find /opt /usr /var -a -type f -name foo.scala</code></td><td>Search specific directories</td></tr><tr><td><mark style="color:yellow;"><code>find /directory* -name foo.txt</code></td><td>Wildcard</td></tr></tbody></table>

Loop: Iterates through each directory and runs the find command inside each, effectively searching them all.

```bash
for dir in /path/to/directory1 /path/to/directory2 ; do
  find "$dir" -name your_search_term
done
```



## <mark style="color:red;">Inverse</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>grep -L</code></td><td>Lists files that do not contain a specified pattern.</td></tr><tr><td><mark style="color:yellow;"><code>ls / | grep -v "[pattern]"</code></td><td>Lists files in the root directory that do not match the specified pattern.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -not -name "[pattern]"</code></td><td>Finds files not matching a specific pattern.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -not -name "*.html"</code></td><td>Finds files that do not end in ".html".</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -name "[pattern]"</code></td><td>An alternative to <mark style="color:yellow;"><code>-not</code>, finds files not matching a specific pattern.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -name "pattern1" ! -name "pattern2"</code></td><td>Finds files not matching multiple patterns.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f ! -exec grep -q "[pattern]" {} \; -print</code></td><td>Finds files that do not contain a specified pattern using <mark style="color:yellow;"><code>-exec</code>.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -print0 | xargs -0 grep -L "[pattern]"</code></td><td>Finds files that do not contain a specified pattern using <mark style="color:yellow;"><code>xargs</code>.</td></tr><tr><td><mark style="color:yellow;"><code>awk '!/[pattern]/' [file]</code></td><td>Uses <mark style="color:yellow;"><code>awk</code> to print lines from a file that do not match a specific pattern.</td></tr><tr><td><mark style="color:yellow;"><code>sed -n '/[pattern]/!p' [file]</code></td><td>Uses <mark style="color:yellow;"><code>sed</code> to print lines from a file that do not match a specific pattern.</td></tr></tbody></table>



## <mark style="color:red;">Weird Filenames</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="496">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -type d -name " \*" -exec ls -ladtri {} 2>/dev/null +</code></td><td>Directories with a space</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name " \*" -exec ls -latriQ {} 2>/dev/null +</code></td><td>Files with a space</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name '*[![:alnum:]_\-\.]*'</code></td><td>Files with non-alphanumeric characters in their filenames.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -regex '.*[^[:alnum:]_\-\.].*'</code></td><td>Files with non-alphanumeric characters in their filenames using regex.</td></tr></tbody></table>



## <mark style="color:red;">Executables</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="494">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>which grep</code></td><td>Single binary</td></tr><tr><td><mark style="color:yellow;"><code>which python java gcc</code></td><td>Multiple binaries</td></tr><tr><td><mark style="color:yellow;"><code>type ls</code></td><td>Shows how the command is interpreted by the shell.</td></tr><tr><td><mark style="color:yellow;"><code>command -v ls</code></td><td>Shows how the command is interpreted by the shell.</td></tr><tr><td><mark style="color:yellow;"><code>which -a python</code></td><td>All instances of "python" in the path.</td></tr></tbody></table>

