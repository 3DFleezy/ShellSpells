# Sort / Compare / Count

Read and insert file content

```bash
sed -r <file>
```

## <mark style="color:red;">Sort</mark>

<table data-header-hidden><thead><tr><th width="255">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sort [file]</code></mark></td><td>Alphabetical, ascending</td></tr><tr><td><mark style="color:yellow;"><code>cat [file] | sort</code></mark></td><td>Pipe output to <mark style="color:yellow;"><code>sort</code></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>sort -n</code></mark></td><td>Sort numerically.</td></tr><tr><td><mark style="color:yellow;"><code>sort -r</code></mark></td><td>Reverses the result of comparisons, producing a descending order sort.</td></tr><tr><td><mark style="color:yellow;"><code>sort -k</code></mark></td><td>Specifies a sort key.</td></tr><tr><td><mark style="color:yellow;"><code>sort -k2</code></mark></td><td>Sorts by second column.</td></tr><tr><td><mark style="color:yellow;"><code>sort -k 2n,2</code></mark></td><td>Sorts numerically based on the second field, ignoring leading whitespace in that field.</td></tr><tr><td><mark style="color:yellow;"><code>sort -k 1b</code></mark></td><td>Sorts by the first word in each line, ignoring case distinctions (<mark style="color:yellow;"><code>-b</code></mark>).</td></tr><tr><td><mark style="color:yellow;"><code>sort -u</code></mark></td><td>Outputs only the first of an equal run.</td></tr><tr><td><mark style="color:yellow;"><code>sort -t</code></mark></td><td>Sets the field delimiter.</td></tr><tr><td><mark style="color:yellow;"><code>sort -t ',' -k 2</code></mark></td><td>Sort lines by the second field</td></tr></tbody></table>

Sorts data.csv first by the second field numerically in descending order, then by the first field ignoring case:

```bash
sort -k 2n,2r -k 1f data.csv
```

Sorts ps output by CPU% descending, then by PID (process ID):

```bash
ps aux | sort -nrk 3,3 -k 8
```

## <mark style="color:red;">Compare</mark>

### <mark style="color:purple;">Choosing the right command</mark>

<table data-header-hidden data-full-width="false"><thead><tr><th width="250">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>diff</code></mark></td><td>For line-by-line text comparison</td></tr><tr><td><mark style="color:yellow;"><code>cmp</code></mark></td><td>For byte-level comparison</td></tr><tr><td><mark style="color:yellow;"><code>comm</code></mark></td><td>For comparing sorted lists</td></tr><tr><td><mark style="color:yellow;"><code>diffstat</code></mark></td><td>For quick statistics</td></tr><tr><td><mark style="color:yellow;"><code>meld</code></mark></td><td>For visual comparison</td></tr><tr><td><mark style="color:yellow;"><code>md5sum</code></mark></td><td>For verifying file integrity</td></tr><tr><td><mark style="color:yellow;"><code>sha256sum</code></mark></td><td>For verifying file integrity</td></tr></tbody></table>

### <mark style="color:purple;">Commands</mark>

<table data-header-hidden data-full-width="false"><thead><tr><th width="403">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>diff &#x3C;file1> &#x3C;file2></code></mark></td><td>Compare two files line by line.</td></tr><tr><td><mark style="color:yellow;"><code>diff -n &#x3C;file1> &#x3C;file2></code></mark></td><td>Suppresses line numbers.</td></tr><tr><td><mark style="color:yellow;"><code>diff -i &#x3C;file1> &#x3C;file2></code></mark></td><td>Ignore case differences in file contents.</td></tr><tr><td><mark style="color:yellow;"><code>diff -u &#x3C;file1> &#x3C;file2></code></mark></td><td>Produce a unified format diff, showing several lines of context.</td></tr><tr><td><mark style="color:yellow;"><code>diff -q &#x3C;file1> &#x3C;file2></code></mark></td><td>Report only when files differ, without detailing the differences.</td></tr><tr><td><mark style="color:yellow;"><code>diff -w &#x3C;file1> &#x3C;file2></code></mark></td><td>Ignore all whitespace changes.</td></tr><tr><td><mark style="color:yellow;"><code>diff -b &#x3C;file1> &#x3C;file2></code></mark></td><td>Ignore changes in the amount of whitespace.</td></tr><tr><td><mark style="color:yellow;"><code>diff --left-column &#x3C;file1> &#x3C;file2></code></mark></td><td>Show line numbers for differences.</td></tr><tr><td><mark style="color:yellow;"><code>cmp &#x3C;file1> &#x3C;file2></code></mark></td><td>Byte-by-byte comparison.</td></tr><tr><td><mark style="color:yellow;"><code>cmp -l &#x3C;file1> &#x3C;file2></code></mark></td><td>Show all differences between the files.</td></tr><tr><td><mark style="color:yellow;"><code>cmp -s &#x3C;file1> &#x3C;file2></code></mark></td><td>Silent mode, do not write anything, just return an exit status.</td></tr><tr><td><mark style="color:yellow;"><code>comm &#x3C;file1> &#x3C;file2></code></mark></td><td>Compare two sorted files line by line.</td></tr><tr><td><mark style="color:yellow;"><code>comm -1 -2 &#x3C;file1> &#x3C;file2></code></mark></td><td>Suppress output of specified columns (1 and 2), showing only lines common to both files.</td></tr><tr><td><mark style="color:yellow;"><code>diff3 &#x3C;file1> &#x3C;file2> file3.txt</code></mark></td><td>Compare three files line by line.</td></tr><tr><td><mark style="color:yellow;"><code>diff3 -m &#x3C;file1> &#x3C;file2> file3.txt</code></mark></td><td>Show only conflicting changes among the three files.</td></tr><tr><td><mark style="color:yellow;"><code>sdiff &#x3C;file1> &#x3C;file2></code></mark></td><td>Side-by-side comparison of files.</td></tr><tr><td><mark style="color:yellow;"><code>sdiff -i &#x3C;file1> &#x3C;file2></code></mark></td><td>Ignore case differences in file contents.</td></tr><tr><td><mark style="color:yellow;"><code>sdiff -s &#x3C;file1> &#x3C;file2></code></mark></td><td>Suppress lines common to both files.</td></tr><tr><td><mark style="color:yellow;"><code>diffstat diff_output</code></mark></td><td>Read a diff output file and display a histogram of insertions, deletions, and modifications per file.</td></tr><tr><td><mark style="color:yellow;"><code>meld file1 file2</code></mark></td><td>Graphical tool to compare and merge files interactively.</td></tr><tr><td><mark style="color:yellow;"><code>md5sum file</code></mark></td><td>Calculate MD5 checksum.</td></tr><tr><td><mark style="color:yellow;"><code>sha256sum file</code></mark></td><td>Calculate SHA-256 checksum.</td></tr></tbody></table>

## <mark style="color:red;">Count</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="523">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>wc [file]</code></mark></td><td>Count lines, words, and bytes.</td></tr><tr><td><mark style="color:yellow;"><code>wc -l [file]</code></mark></td><td>Count lines.</td></tr><tr><td><mark style="color:yellow;"><code>wc -w [file]</code></mark></td><td>Count words.</td></tr><tr><td><mark style="color:yellow;"><code>wc -c [file]</code></mark></td><td>Count bytes.</td></tr><tr><td><mark style="color:yellow;"><code>wc -m [file]</code></mark></td><td>Count characters.</td></tr><tr><td><mark style="color:yellow;"><code>awk 'END {print NR}' [file]</code></mark></td><td>Count lines. <mark style="color:yellow;"><code>NR</code></mark> represents the total number of records processed.</td></tr><tr><td><mark style="color:yellow;"><code>awk '{count++} END {print count}' [file]</code></mark></td><td>Count lines.</td></tr><tr><td><mark style="color:yellow;"><code>awk '/error/ {count++} END {print count}' [file]</code></mark></td><td>Count lines containing "error".</td></tr><tr><td><mark style="color:yellow;"><code>sed '/^$/d' filename | wc -l</code></mark></td><td>Counts non-empty lines.</td></tr><tr><td><mark style="color:yellow;"><code>sed 's/[^a-zA-Z0-9 ]//g' filename | wc -w</code></mark></td><td>Counts alphanumeric words</td></tr><tr><td><mark style="color:yellow;"><code>sed -n '$=' [file]</code></mark></td><td>Count lines. <mark style="color:yellow;"><code>$=</code></mark> command prints the total number of lines.</td></tr><tr><td><mark style="color:yellow;"><code>grep pattern [file] | wc -l</code></mark></td><td>Alternate way to count lines</td></tr><tr><td><mark style="color:yellow;"><code>grep -c "[pattern]" [file]</code></mark></td><td>Lines with pattern match.</td></tr><tr><td><mark style="color:yellow;"><code>grep -c "[pattern]" &#x3C;file1> &#x3C;file2></code></mark></td><td>Miltiple files</td></tr><tr><td><mark style="color:yellow;"><code>grep -o "[pattern]" [file] | wc -l</code></mark></td><td>Count pattern matches, including multiple occurrences per line. <mark style="color:yellow;"><code>-o</code></mark> outputs each match on a new line.</td></tr><tr><td><mark style="color:yellow;"><code>grep -r -c "[pattern]" /directory</code></mark></td><td>Recursive counts lines with pattern match.</td></tr><tr><td><mark style="color:yellow;"><code>find . -type f | wc -l</code></mark></td><td>Count files in a directory and its subdirectories</td></tr></tbody></table>

Recursive by file extension:

```bash
grep --include=\*.<ext> -ro "[pattern]" <directory> | wc -l
```

Recursive counts lines with pattern match:

```bash
find / -type f -exec grep -o "[pattern]" {} + | wc -l
```

Uses `awk` to globally substitute (thus count) occurrences of the pattern in each line and sums them up:

```bash
awk '{count += gsub(/[pattern]/, "[pattern]")} END {print count}' [file]
```

Count the total number of lines across all files in a directory and its subdirectories:

```bash
find . -type f -exec wc -l {} + | awk '{total += $1} END {print total}'
```
