# Modify Content

Note: `sed -i` will change original file.

## <mark style="color:red;">Overwrite</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="598">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>cat > file</code></td><td>Overwrite/create file</td></tr><tr><td><mark style="color:yellow;"><code>echo "text" > [file]</code></td><td>Overwrite/create file</td></tr><tr><td><mark style="color:yellow;"><code>echo "text" | tee [file]</code></td><td>Overwrite/create file and display</td></tr><tr><td><mark style="color:yellow;"><code>printf "Line 1\nLine 2" > [file]</code></td><td>Overwrite/create file with newlines.</td></tr><tr><td><mark style="color:yellow;"><code>awk -v text="some text" 'BEGIN{print text > "filename"}'</code></td><td>Overwrite/create file</td></tr><tr><td><mark style="color:yellow;"><code>echo "text" | dd of=file</code></td><td>Write "text" to <mark style="color:yellow;"><code>file</code> using <mark style="color:yellow;"><code>dd</code>, overwriting existing contents.</td></tr></tbody></table>

## <mark style="color:red;">Insert</mark>

### <mark style="color:purple;">Strings</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="600">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>echo "text" >> [file]</code></td><td>Append "text" to the end of a file.</td></tr><tr><td><mark style="color:yellow;"><code>sed i\text</code></td><td>Before each line</td></tr><tr><td><mark style="color:yellow;"><code>sed a\text</code></td><td>After each line</td></tr><tr><td><mark style="color:yellow;"><code>sed '$ a\text' [file]</code></td><td>Use <mark style="color:yellow;"><code>sed</code> to insert "text" at the end of a file.</td></tr><tr><td><mark style="color:yellow;"><code>sed '$a text' file</code></td><td>Append "text" at the end of <mark style="color:yellow;"><code>file</code>.</td></tr><tr><td><mark style="color:yellow;"><code>sed '1i text' file</code></td><td>Insert "text" at the beginning of <mark style="color:yellow;"><code>file</code></td></tr><tr><td><mark style="color:yellow;"><code>awk 'END {print "text"} 1' file > temp &#x26;&#x26; mv temp [file]</code></td><td>Append "text" at the end of a file.</td></tr></tbody></table>

### <mark style="color:purple;">Lines</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sed '1i\New line' [file]</code></td><td>Insert newline at beginning</td></tr><tr><td><mark style="color:yellow;"><code>sed '$a\New line' [file]</code></td><td>Append new line at the end</td></tr><tr><td><mark style="color:yellow;"><code>sed '/pattern/a\new line' file</code></td><td>Append new line after lines with pattern</td></tr><tr><td><mark style="color:yellow;"><code>sed G [file]</code></td><td>Adds blank line between lines (Double Space)</td></tr><tr><td><mark style="color:yellow;"><code>nl -ba file > temp &#x26;&#x26; mv temp file</code></td><td>Add line numbers to each line.</td></tr><tr><td><mark style="color:yellow;"><code>awk '{print NR, $0}' file > temp &#x26;&#x26; mv temp file</code></td><td>Add line numbers to each line.</td></tr></tbody></table>

### <mark style="color:purple;">Append</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="557">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>cat >> file</code></td><td>Append to <mark style="color:yellow;"><code>file</code> from stdin until EOF (Ctrl+D).</td></tr><tr><td><mark style="color:yellow;"><code>echo "text" | tee -a [file]</code></td><td>Append and display</td></tr><tr><td><mark style="color:yellow;"><code>printf "text" >> [file]</code></td><td>Append</td></tr><tr><td><mark style="color:yellow;"><code>awk -v text="more text" '{print $0 ORS text}' [file]</code></td><td>Append?</td></tr></tbody></table>

## <mark style="color:red;">Replace / Remove</mark>

### <mark style="color:purple;">Replace Strings</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="426">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sed 's/pattern/new/' [file]</code></td><td>Replace pattern with new in file.txt</td></tr><tr><td><mark style="color:yellow;"><code>sed 's/pattern/new/g' [file]</code></td><td>Replace all occurrences of "old" with "new".</td></tr><tr><td><mark style="color:yellow;"><code>sed 's/pattern/new/2' [file]</code></td><td>Replace 2nd pattern in a line.</td></tr><tr><td><mark style="color:yellow;"><code>sed '2 s/pattern/new/' [file]</code></td><td>Replace pattern on line 2</td></tr><tr><td><mark style="color:yellow;"><code>sed 1,5s/pattern/new/ [file]</code></td><td>Replace pattern on lines 1 to 5</td></tr><tr><td><mark style="color:yellow;"><code>sed /pattern/, /pattern2/s/old/new/</code></td><td>Replace between two patterns</td></tr><tr><td><mark style="color:yellow;"><code>sed $s/pattern/new/</code></td><td>Replace pattern on last line</td></tr><tr><td><mark style="color:yellow;"><code>sed 's/,/\n/g' file</code></td><td>Replace Commas with Newline</td></tr><tr><td><mark style="color:yellow;"><code>tr , '\n' &#x3C; file</code></td><td>Replace Commas with Newline</td></tr></tbody></table>

Replaces occurrences of 'old\_pattern' with 'new\_pattern' and prints each line:

```bash
awk '{gsub(/old_pattern/, "new_pattern"); print}' [file]
```

Globally replace "old" with "new" in a file.

```bash
awk '{gsub(/old/, "new"); print}' [file] > temp && mv temp [file]
```

Finds and replaces text within a specified range:

```bash
awk '/start_pattern/, /end_pattern/ {gsub(/old_pattern/, "new_pattern"); print}' [file]
```

Use `perl` to replace "old" with "new" in a file, similar to `sed`:

```bash
perl -pi -e 's/old/new/g' [file]
```

### <mark style="color:purple;">Remove Strings</mark>

| Command                    | Description                          |
| -------------------------- | ------------------------------------ |
| <mark style="color:yellow;">`cut -f 1 -d $'\t' [file]`</mark> | Suppressing Non-Printable Characters |

### <mark style="color:purple;">Remove Lines</mark>

#### <mark style="color:green;">Patterns</mark>

<table data-header-hidden data-full-width="false"><thead><tr><th width="495">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sed '/pattern/d' file</code></td><td>Remove lines matching "pattern".</td></tr><tr><td><mark style="color:yellow;"><code>awk '!/pattern/' file > temp &#x26;&#x26; mv temp file</code></td><td>Remove lines matching "pattern".</td></tr><tr><td><mark style="color:yellow;"><code>grep -v "pattern" file > temp &#x26;&#x26; mv temp file</code></td><td>Use <mark style="color:yellow;"><code>grep</code> with <mark style="color:yellow;"><code>-v</code> to filter out lines matching "pattern".</td></tr></tbody></table>

#### <mark style="color:green;">Line Numbers</mark>

| Command | Description |
| -------------------- | ---------------------------- |
| <mark style="color:yellow;">`sed '/^9/d' [file]`</mark> | Delete lines starting with 9 |
| <mark style="color:yellow;">`sed '1,3d' [file]`</mark>  | Delete lines 1 to 3          |

#### <mark style="color:green;">Blank Lines</mark>

<table data-header-hidden><thead><tr><th width="456">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sed '/^$/d' [file]</code></td><td>Remove blank lines.</td></tr><tr><td><mark style="color:yellow;"><code>sed 'n;d'</code></td><td>Remove blank lines between lines (Double Spaced) (assumes even numbered lines are blank)</td></tr><tr><td><mark style="color:yellow;"><code>awk 'NF' [file] > temp &#x26;&#x26; mv temp [file]</code></td><td>Remove blank lines, keeping lines with at least one field.</td></tr></tbody></table>

#### <mark style="color:green;">Duplicate Lines</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>awk '!seen[$0]++' file > temp &#x26;&#x26; mv temp file</code></td><td>Remove duplicate lines, preserving the order.</td></tr><tr><td><mark style="color:yellow;"><code>sort -u file > temp &#x26;&#x26; mv temp file</code></td><td>Sort the file and remove duplicate lines, may change the original order.</td></tr></tbody></table>

#### <mark style="color:green;">Comment Lines</mark>

Removing lines that start with `#`. E ssentially this removes all the comments out of a file. This is good when examining a config file full of comments when you just want to see a certain line.

```bash
cat <file> |  grep -v ^\# | grep .
```

```bash
sed '/^#/d' <file>
```

## <mark style="color:red;">Convert Case</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="599">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>tr '[:upper:]' '[:lower:]' &#x3C; file > temp &#x26;&#x26; mv temp file</code></td><td>Convert all text to lowercase.</td></tr><tr><td><mark style="color:yellow;"><code>tr '[:lower:]' '[:upper:]' &#x3C; file > temp &#x26;&#x26; mv temp file</code></td><td>Convert all text to uppercase.</td></tr><tr><td><mark style="color:yellow;"><code>awk '{print tolower($0)}' file > temp &#x26;&#x26; mv temp file</code></td><td>Convert all text to lowercase using <mark style="color:yellow;"><code>awk</code>.</td></tr><tr><td><mark style="color:yellow;"><code>awk '{print toupper($0)}' file > temp &#x26;&#x26; mv temp file</code></td><td>Convert all text to uppercase using <mark style="color:yellow;"><code>awk</code>.</td></tr></tbody></table>

## <mark style="color:red;">Text Editors</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="171">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>vim file</code></td><td>Open <mark style="color:yellow;"><code>file</code> in Vim editor for editing. Save and exit with <mark style="color:yellow;"><code>:wq</code>.</td></tr><tr><td><mark style="color:yellow;"><code>nano file</code></td><td>Open <mark style="color:yellow;"><code>file</code> in Nano editor for editing. Save and exit with <mark style="color:yellow;"><code>Ctrl+O</code>, <mark style="color:yellow;"><code>Ctrl+X</code>.</td></tr><tr><td><mark style="color:yellow;"><code>emacs file</code></td><td>Open <mark style="color:yellow;"><code>file</code> in Emacs editor for editing. Save with <mark style="color:yellow;"><code>Ctrl+x Ctrl+s</code> and exit with <mark style="color:yellow;"><code>Ctrl+x Ctrl+c</code>.</td></tr></tbody></table>
