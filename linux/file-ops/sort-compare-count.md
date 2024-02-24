# Sort / Compare / Count

| Command         | Description                   |
| --------------- | ----------------------------- |
| `sed -r [file]` | Read and insert file content. |

## Sort

| Command              | Description                                                                             |
| -------------------- | --------------------------------------------------------------------------------------- |
| `sort [file]`        | Alphabetical, ascending                                                                 |
| `cat [file] \| sort` | Pipe output to `sort`.                                                                  |
| `sort -n`            | Sort numerically.                                                                       |
| `sort -r`            | Reverses the result of comparisons, producing a descending order sort.                  |
| `sort -k`            | Specifies a sort key.                                                                   |
| `sort -k2`           | Sorts by second column.                                                                 |
| `sort -k 2n,2`       | Sorts numerically based on the second field, ignoring leading whitespace in that field. |
| `sort -k 1b`         | Sorts by the first word in each line, ignoring case distinctions (`-b`).                |
| `sort -u`            | Outputs only the first of an equal run.                                                 |
| `sort -t`            | Sets the field delimiter.                                                               |
| `sort -t ',' -k 2`   | Sort lines by the second field                                                          |

Sorts data.csv first by the second field numerically in descending order, then by the first field ignoring case:

```bash
sort -k 2n,2r -k 1f data.csv
```

Sorts ps output by CPU% descending, then by PID (process ID):

```bash
ps aux | sort -nrk 3,3 -k 8
```

## Compare

### Choosing the right command

| Command     | Description                      |
| ----------- | -------------------------------- |
| `diff`      | For line-by-line text comparison |
| `cmp`       | For byte-level comparison        |
| `comm`      | For comparing sorted lists       |
| `diffstat`  | For quick statistics             |
| `meld`      | For visual comparison            |
| `md5sum`    | For verifying file integrity     |
| `sha256sum` | For verifying file integrity     |

### Commands

| Command                              | Description                                                                                           |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| `diff <file1> <file2>`               | Compare two files line by line.                                                                       |
| `diff -n <file1> <file2>`            | Suppresses line numbers.                                                                              |
| `diff -i <file1> <file2>`            | Ignore case differences in file contents.                                                             |
| `diff -u <file1> <file2>`            | Produce a unified format diff, showing several lines of context.                                      |
| `diff -q <file1> <file2>`            | Report only when files differ, without detailing the differences.                                     |
| `diff -w <file1> <file2>`            | Ignore all whitespace changes.                                                                        |
| `diff -b <file1> <file2>`            | Ignore changes in the amount of whitespace.                                                           |
| `diff --left-column <file1> <file2>` | Show line numbers for differences.                                                                    |
| `cmp <file1> <file2>`                | Byte-by-byte comparison.                                                                              |
| `cmp -l <file1> <file2>`             | Show all differences between the files.                                                               |
| `cmp -s <file1> <file2>`             | Silent mode, do not write anything, just return an exit status.                                       |
| `comm <file1> <file2>`               | Compare two sorted files line by line.                                                                |
| `comm -1 -2 <file1> <file2>`         | Suppress output of specified columns (1 and 2), showing only lines common to both files.              |
| `diff3 <file1> <file2> file3.txt`    | Compare three files line by line.                                                                     |
| `diff3 -m <file1> <file2> file3.txt` | Show only conflicting changes among the three files.                                                  |
| `sdiff <file1> <file2>`              | Side-by-side comparison of files.                                                                     |
| `sdiff -i <file1> <file2>`           | Ignore case differences in file contents.                                                             |
| `sdiff -s <file1> <file2>`           | Suppress lines common to both files.                                                                  |
| `diffstat diff_output`               | Read a diff output file and display a histogram of insertions, deletions, and modifications per file. |
| `meld file1 file2`                   | Graphical tool to compare and merge files interactively.                                              |
| `md5sum file`                        | Calculate MD5 checksum.                                                                               |
| `sha256sum file`                     | Calculate SHA-256 checksum.                                                                           |

## Count

| Command                                            | Description                                                                                            |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `wc [file]`                                        | Count lines, words, and bytes.                                                                         |
| `wc -l [file]`                                     | Count lines.                                                                                           |
| `wc -w [file]`                                     | Count words.                                                                                           |
| `wc -c [file]`                                     | Count bytes.                                                                                           |
| `wc -m [file]`                                     | Count characters.                                                                                      |
| `awk 'END {print NR}' [file]`                      | Count lines. `NR` represents the total number of records processed.                                    |
| `awk '{count++} END {print count}' [file]`         | Count lines.                                                                                           |
| `awk '/error/ {count++} END {print count}' [file]` | Count lines containing "error".                                                                        |
| `sed '/^$/d' filename \| wc -l`                    | Counts non-empty lines.                                                                                |
| `sed 's/[^a-zA-Z0-9 ]//g' filename \| wc -w`       | Counts alphanumeric words                                                                              |
| `sed -n '$=' [file]`                               | Count lines. `$=` command prints the total number of lines.                                            |
| `grep pattern [file] \| wc -l`                     | Alternate way to count lines                                                                           |
| `grep -c "[pattern]" [file]`                       | Lines with pattern match.                                                                              |
| `grep -c "[pattern]" <file1> <file2>`              | Miltiple files                                                                                         |
| `grep -o "[pattern]" [file] \| wc -l`              | Count pattern matches, including multiple occurrences per line. `-o` outputs each match on a new line. |
| `grep -r -c "[pattern]" /directory`                | Recursive counts lines with pattern match.                                                             |
| `find . -type f \| wc -l`                          | Count files in a directory and its subdirectories                                                      |

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
