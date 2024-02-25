# Filename

## <mark style="color:red;">Filenames</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="420">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>grep -rli file*</code></mark></td><td>Pattern match</td></tr><tr><td><mark style="color:yellow;"><code>grep -rli "filename" /path/to/search</code></mark></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>ls -R [directory] | grep "filename"</code></mark></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -iname "filename"</code></mark></td><td>Case insensitive</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name password.txt</code></mark></td><td>Recursive exact match</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -name "pat*tern"</code></mark></td><td>Pattern match "pat" and ending with "tern"</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type d -name config</code></mark></td><td>Exact directory match</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type d -name "\*687-250\*"</code></mark></td><td>Pattern directory match</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -regex "regex_pattern"</code></mark></td><td>Regex</td></tr><tr><td><mark style="color:yellow;"><code>locate "[filename]"</code></mark></td><td>Uses a database updated by <mark style="color:yellow;"><code>updatedb</code></mark> to quickly locate files</td></tr><tr><td><mark style="color:yellow;"><code>locate -i "[filename]"</code></mark></td><td>Case-insensitive</td></tr></tbody></table>

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

<table data-header-hidden data-full-width="true"><thead><tr><th width="572">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ls [directory]/*.ext</code></mark></td><td>Not Recursive</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f \( -name "*.txt" -o -name "*.sh" \)</code></mark></td><td>Multiple file extensions.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name "*.txt"</code></mark></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -iname "*.txt"</code></mark></td><td>Case-insensitive.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -regex ".*\.txt"</code></mark></td><td>Use regular expressions.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -regextype posix -regex ".+\.log$"</code></mark></td><td>Matches all files ending with .log, using POSIX regex syntax.</td></tr><tr><td><mark style="color:yellow;"><code>grep -rli "\.txt$" /path/to/search</code></mark></td><td>Recursive</td></tr><tr><td><mark style="color:yellow;"><code>grep -rli --include=\*.ext "pattern" [directory]</code></mark></td><td>Recursively searches for files with the <mark style="color:yellow;"><code>.ext</code></mark> extension containing "pattern" in the specified directory.</td></tr></tbody></table>

## <mark style="color:red;">Search Multiple Dirs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find /opt /usr /var -a -type f -name foo.scala</code></mark></td><td>Search specific directories</td></tr><tr><td><mark style="color:yellow;"><code>find /directory* -name foo.txt</code></mark></td><td>Wildcard</td></tr></tbody></table>

Loop: Iterates through each directory and runs the find command inside each, effectively searching them all.

```bash
for dir in /path/to/directory1 /path/to/directory2 ; do
  find "$dir" -name your_search_term
done
```

## <mark style="color:red;">Inverse</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>grep -L</code></mark></td><td>Lists files that do not contain a specified pattern.</td></tr><tr><td><mark style="color:yellow;"><code>ls / | grep -v "[pattern]"</code></mark></td><td>Lists files in the root directory that do not match the specified pattern.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -not -name "[pattern]"</code></mark></td><td>Finds files not matching a specific pattern.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -not -name "*.html"</code></mark></td><td>Finds files that do not end in ".html".</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -name "[pattern]"</code></mark></td><td>An alternative to <mark style="color:yellow;"><code>-not</code></mark>, finds files not matching a specific pattern.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a ! -name "pattern1" ! -name "pattern2"</code></mark></td><td>Finds files not matching multiple patterns.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f ! -exec grep -q "[pattern]" {} \; -print</code></mark></td><td>Finds files that do not contain a specified pattern using <mark style="color:yellow;"><code>-exec</code></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -print0 | xargs -0 grep -L "[pattern]"</code></mark></td><td>Finds files that do not contain a specified pattern using <mark style="color:yellow;"><code>xargs</code></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>awk '!/[pattern]/' [file]</code></mark></td><td>Uses <mark style="color:yellow;"><code>awk</code></mark> to print lines from a file that do not match a specific pattern.</td></tr><tr><td><mark style="color:yellow;"><code>sed -n '/[pattern]/!p' [file]</code></mark></td><td>Uses <mark style="color:yellow;"><code>sed</code></mark> to print lines from a file that do not match a specific pattern.</td></tr></tbody></table>

## <mark style="color:red;">Weird Filenames</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="496">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -a -type d -name " \*" -exec ls -ladtri {} 2>/dev/null +</code></mark></td><td>Directories with a space</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name " \*" -exec ls -latriQ {} 2>/dev/null +</code></mark></td><td>Files with a space</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name '*[![:alnum:]_\-\.]*'</code></mark></td><td>Files with non-alphanumeric characters in their filenames.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -regex '.*[^[:alnum:]_\-\.].*'</code></mark></td><td>Files with non-alphanumeric characters in their filenames using regex.</td></tr></tbody></table>

## <mark style="color:red;">Executables</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="494">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>which grep</code></mark></td><td>Single binary</td></tr><tr><td><mark style="color:yellow;"><code>which python java gcc</code></mark></td><td>Multiple binaries</td></tr><tr><td><mark style="color:yellow;"><code>type ls</code></mark></td><td>Shows how the command is interpreted by the shell.</td></tr><tr><td><mark style="color:yellow;"><code>command -v ls</code></mark></td><td>Shows how the command is interpreted by the shell.</td></tr><tr><td><mark style="color:yellow;"><code>which -a python</code></mark></td><td>All instances of "python" in the path.</td></tr></tbody></table>
