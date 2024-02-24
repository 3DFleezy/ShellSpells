# Sort / Compare / Count

Read and insert file content

```bash
sed -r <file>
```

## <mark style="color:red;">Sort</mark>

<table data-header-hidden><thead><tr><th width="255">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sort [file]</code></td><td>Alphabetical, ascending</td></tr><tr><td><code>cat [file] | sort</code></td><td>Pipe output to <code>sort</code>.</td></tr><tr><td><code>sort -n</code></td><td>Sort numerically.</td></tr><tr><td><code>sort -r</code></td><td>Reverses the result of comparisons, producing a descending order sort.</td></tr><tr><td><code>sort -k</code></td><td>Specifies a sort key.</td></tr><tr><td><code>sort -k2</code></td><td>Sorts by second column.</td></tr><tr><td><code>sort -k 2n,2</code></td><td>Sorts numerically based on the second field, ignoring leading whitespace in that field.</td></tr><tr><td><code>sort -k 1b</code></td><td>Sorts by the first word in each line, ignoring case distinctions (<code>-b</code>).</td></tr><tr><td><code>sort -u</code></td><td>Outputs only the first of an equal run.</td></tr><tr><td><code>sort -t</code></td><td>Sets the field delimiter.</td></tr><tr><td><code>sort -t ',' -k 2</code></td><td>Sort lines by the second field</td></tr></tbody></table>

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

<table data-header-hidden data-full-width="false"><thead><tr><th width="250">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>diff</code></td><td>For line-by-line text comparison</td></tr><tr><td><code>cmp</code></td><td>For byte-level comparison</td></tr><tr><td><code>comm</code></td><td>For comparing sorted lists</td></tr><tr><td><code>diffstat</code></td><td>For quick statistics</td></tr><tr><td><code>meld</code></td><td>For visual comparison</td></tr><tr><td><code>md5sum</code></td><td>For verifying file integrity</td></tr><tr><td><code>sha256sum</code></td><td>For verifying file integrity</td></tr></tbody></table>

### <mark style="color:purple;">Commands</mark>

<table data-header-hidden data-full-width="false"><thead><tr><th width="403">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>diff &#x3C;file1> &#x3C;file2></code></td><td>Compare two files line by line.</td></tr><tr><td><code>diff -n &#x3C;file1> &#x3C;file2></code></td><td>Suppresses line numbers.</td></tr><tr><td><code>diff -i &#x3C;file1> &#x3C;file2></code></td><td>Ignore case differences in file contents.</td></tr><tr><td><code>diff -u &#x3C;file1> &#x3C;file2></code></td><td>Produce a unified format diff, showing several lines of context.</td></tr><tr><td><code>diff -q &#x3C;file1> &#x3C;file2></code></td><td>Report only when files differ, without detailing the differences.</td></tr><tr><td><code>diff -w &#x3C;file1> &#x3C;file2></code></td><td>Ignore all whitespace changes.</td></tr><tr><td><code>diff -b &#x3C;file1> &#x3C;file2></code></td><td>Ignore changes in the amount of whitespace.</td></tr><tr><td><code>diff --left-column &#x3C;file1> &#x3C;file2></code></td><td>Show line numbers for differences.</td></tr><tr><td><code>cmp &#x3C;file1> &#x3C;file2></code></td><td>Byte-by-byte comparison.</td></tr><tr><td><code>cmp -l &#x3C;file1> &#x3C;file2></code></td><td>Show all differences between the files.</td></tr><tr><td><code>cmp -s &#x3C;file1> &#x3C;file2></code></td><td>Silent mode, do not write anything, just return an exit status.</td></tr><tr><td><code>comm &#x3C;file1> &#x3C;file2></code></td><td>Compare two sorted files line by line.</td></tr><tr><td><code>comm -1 -2 &#x3C;file1> &#x3C;file2></code></td><td>Suppress output of specified columns (1 and 2), showing only lines common to both files.</td></tr><tr><td><code>diff3 &#x3C;file1> &#x3C;file2> file3.txt</code></td><td>Compare three files line by line.</td></tr><tr><td><code>diff3 -m &#x3C;file1> &#x3C;file2> file3.txt</code></td><td>Show only conflicting changes among the three files.</td></tr><tr><td><code>sdiff &#x3C;file1> &#x3C;file2></code></td><td>Side-by-side comparison of files.</td></tr><tr><td><code>sdiff -i &#x3C;file1> &#x3C;file2></code></td><td>Ignore case differences in file contents.</td></tr><tr><td><code>sdiff -s &#x3C;file1> &#x3C;file2></code></td><td>Suppress lines common to both files.</td></tr><tr><td><code>diffstat diff_output</code></td><td>Read a diff output file and display a histogram of insertions, deletions, and modifications per file.</td></tr><tr><td><code>meld file1 file2</code></td><td>Graphical tool to compare and merge files interactively.</td></tr><tr><td><code>md5sum file</code></td><td>Calculate MD5 checksum.</td></tr><tr><td><code>sha256sum file</code></td><td>Calculate SHA-256 checksum.</td></tr></tbody></table>

## <mark style="color:red;">Count</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="523">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>wc [file]</code></td><td>Count lines, words, and bytes.</td></tr><tr><td><code>wc -l [file]</code></td><td>Count lines.</td></tr><tr><td><code>wc -w [file]</code></td><td>Count words.</td></tr><tr><td><code>wc -c [file]</code></td><td>Count bytes.</td></tr><tr><td><code>wc -m [file]</code></td><td>Count characters.</td></tr><tr><td><code>awk 'END {print NR}' [file]</code></td><td>Count lines. <code>NR</code> represents the total number of records processed.</td></tr><tr><td><code>awk '{count++} END {print count}' [file]</code></td><td>Count lines.</td></tr><tr><td><code>awk '/error/ {count++} END {print count}' [file]</code></td><td>Count lines containing "error".</td></tr><tr><td><code>sed '/^$/d' filename | wc -l</code></td><td>Counts non-empty lines.</td></tr><tr><td><code>sed 's/[^a-zA-Z0-9 ]//g' filename | wc -w</code></td><td>Counts alphanumeric words</td></tr><tr><td><code>sed -n '$=' [file]</code></td><td>Count lines. <code>$=</code> command prints the total number of lines.</td></tr><tr><td><code>grep pattern [file] | wc -l</code></td><td>Alternate way to count lines</td></tr><tr><td><code>grep -c "[pattern]" [file]</code></td><td>Lines with pattern match.</td></tr><tr><td><code>grep -c "[pattern]" &#x3C;file1> &#x3C;file2></code></td><td>Miltiple files</td></tr><tr><td><code>grep -o "[pattern]" [file] | wc -l</code></td><td>Count pattern matches, including multiple occurrences per line. <code>-o</code> outputs each match on a new line.</td></tr><tr><td><code>grep -r -c "[pattern]" /directory</code></td><td>Recursive counts lines with pattern match.</td></tr><tr><td><code>find . -type f | wc -l</code></td><td>Count files in a directory and its subdirectories</td></tr></tbody></table>

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
