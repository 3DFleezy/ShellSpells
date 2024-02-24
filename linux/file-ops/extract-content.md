# Extract Content

## <mark style="color:red;">Basic Pattern Match</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="394">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>cat [file] | grep "string"</code></td><td>Lines with match</td></tr><tr><td><code>sed /pattern/ [file]</code></td><td>Lines with match</td></tr><tr><td><code>sed -n '/[pattern]/p' [file]</code></td><td>Lines with match</td></tr><tr><td><code>awk '/[pattern]/' [file]</code></td><td>Lines with match</td></tr><tr><td><code>grep "string" [file]</code></td><td>Lines with match</td></tr><tr><td><code>grep -i "string" [file]</code></td><td>Case insensitive</td></tr><tr><td><code>grep -E "&#x3C;regex>" [file]</code></td><td>Uses extended regular expressions for pattern matching.</td></tr><tr><td><code>grep -w "string" [file]</code></td><td>Print all lines with the whole word matching the string pattern.</td></tr><tr><td><code>grep "\\bstring\\b" [file]</code></td><td>Print all lines with string pattern match with a space before or after.</td></tr><tr><td><code>grep "string1?" [file]</code></td><td>? = optional. Prints lines that match at least 1 time</td></tr><tr><td><code>grep "string1\*" [file]</code></td><td>The character proceeding the "*" is optional</td></tr><tr><td><code>grep "string1+" [file]</code></td><td>The character proceeding the "+" is optional. Optional character must match at least 1 time</td></tr><tr><td><code>grep -P "&#x3C;perl_regex>" [file]</code></td><td>Uses Perl-compatible regular expressions for pattern matching (if supported by <code>grep</code>).</td></tr></tbody></table>

## <mark style="color:red;">Exact Line Match</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>grep -x "entire line" [file]</code></td><td>Lines that exactly match the whole pattern</td></tr></tbody></table>

## <mark style="color:red;">Strings (Not lines)</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="529">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>grep -o "pattern" [file]</code></td><td>Extract and print only the parts of a line that match the "pattern".</td></tr><tr><td><code>egrep -o "pattern" [file]</code></td><td>Similar to <code>grep -o</code>, but supports extended regular expressions for more complex patterns.</td></tr><tr><td><code>sed -n 's/.*pattern\(.*\)/\1/p' [file]</code></td><td>Extract and print text following "pattern".</td></tr><tr><td><code>cut -d':' -f1 [file]</code></td><td>Extract and print the first field from lines, assuming ':' delimiter.</td></tr><tr><td><code>sed -n 's/.*pattern\(.*\)/\1/p' [file]</code></td><td>Extract and print text following "pattern".</td></tr><tr><td><code>perl -ne 'print "$1\n" if /.*pattern(.*)/' [file]</code></td><td>Extract and print text following "pattern".</td></tr></tbody></table>

## <mark style="color:red;">Start/End of Line</mark>

| `grep "^string" [file]` | Start with pattern match |
| ----------------------- | ------------------------ |
| `sed /^pattern/ [file]` | Start with pattern match |
| `grep "string$" [file]` | End with pattern match   |
| `sed /pattern$/ [file]` | End with pattern match   |

## <mark style="color:red;">Columns/Fields</mark>

| `awk '{print $1, $3}' [file]`      | Prints the first and third columns of each line in the file          |
| ---------------------------------- | -------------------------------------------------------------------- |
| `awk '/pattern/{print $2}' [file]` | Prints the second column of lines containing the specified pattern   |
| `awk '$2 > 50 {print}' [file]`     | Prints lines where the value in the second column is greater than 50 |
| `awk '!seen[$1]++' [file]`         | Prints unique values in the first column                             |
| `cut -f 1,3 -d ',' data.csv`       | Cutting Specific Fields                                              |
| `cut -f 2-4 -d ':' /etc/passwd`    | Cutting by Range and Delimiter                                       |
| `cut -f 2-4,6-8 -d ' ' log.txt`    | Cutting multiple field ranges                                        |
| `cut -f 1 -d ':;,' [file]`         | Cutting Multiple Delimiters                                          |
| `cut -f 2 -d ' ' [file]`           | Cutting by Whitespace                                                |
| `cut -f 2- --complement data.csv`  | Displaying Complement of Fields                                      |

Uses `grep` to find matching lines, then `awk` to print the second field of those lines:

```bash
grep "[pattern]" filename | awk '{print $2}'
```

### <mark style="color:purple;">Delimiters</mark>

Specifies a custom delimiter (':' in this case) and prints the first column.

```bash
awk -F':' '{print $1}' filename
```

Cutting with Custom Delimiter

```bash
cut -f 1 -d '|' data.txt
```

```bash
cut -f <fields> -d <delimiter> [filename]
```

| Option           | Description                               |
| ---------------- | ----------------------------------------- |
| `-f <fields>`    | Specify the fields to cut (e.g., -f 1,3). |
| `-d <delimiter>` | Set the delimiter that separates fields.  |
| `-c <character>` | Character Position                        |
| `-b <bytes>`     | Byte position                             |

### <mark style="color:purple;">Calculate Sum of Column</mark>

Calculates and prints the sum of values in the third column.

```bash
awk '{sum+=$3} END {print sum}' filename
```

Groups data by the first column and prints the sum of the third column for each group.

```bash
awk '{sum[$1]+=$3} END {for (i in sum) print i, sum[i]}' filename
```

Uses AWK as a calculator to perform arithmetic operations.

```bash
awk 'BEGIN{result = 10 + 5; print "Result:", result}'
```

### <mark style="color:purple;">Print Rows with Max Value in a Column</mark>

Identifies and prints the row with the maximum value in the third column.

```bash
awk '{if ($3 > max) {max=$3; row=$0}} END {print row}' filename
```

### <mark style="color:purple;">Format Column Width</mark>

```bash
awk '{printf "%-10s %-8s\n", $1, $2}' filename `| Formats and prints the first two columns with specific width.
```

## <mark style="color:red;">Limit Matches</mark>

Stop reading after finding 4 string pattern matches:

```bash
grep -m 4 "string" [file]
```

## <mark style="color:red;">Multiple Patterns</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>grep -E "string1|string2|string3" [file]</code></td><td>Search for 2 or more pattern matches using extended grep</td></tr><tr><td><code>egrep "pattern1|pattern2|pattern3" [file]</code></td><td>Search for 2 or more pattern matches using extended grep</td></tr><tr><td><code>grep -e "string1" -e "string2" -e "string3" [file]</code></td><td>Search for 2 or more pattern matches.</td></tr><tr><td><code>sed /pattern1/p; /pattern2/p [file]</code></td><td>Search for 2 separate pattern matches using sed.</td></tr></tbody></table>

## <mark style="color:red;">Characters</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="530">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>cut -c1-10 [file]</code></td><td>Extracts the first 10 characters of each line.</td></tr><tr><td><code>awk '{print substr($0, 1, 10)}' [file]</code></td><td>Extracts the first 10 characters of each line.</td></tr><tr><td><code>cut -c5,7,9 [file]</code></td><td>Extracts the 5th, 7th, and 9th characters of each line.</td></tr><tr><td><code>awk '{print substr($0, 5, 1) substr($0, 7, 1) substr($0, 9, 1)}' [file]</code></td><td>Extracts the 5th, 7th, and 9th characters of each line.</td></tr><tr><td><code>awk '{print substr($0, length($0), 1)}' [file]</code></td><td>Extracts the last character of each line.</td></tr><tr><td><code>sed 's/.*\(.\)$/\1/' [file]</code></td><td>Extracts the last character of each line.</td></tr><tr><td><code>grep "[[:digit:]]" [file]</code></td><td>Prints all lines containing digits.</td></tr><tr><td><code>grep "[[:upper:]]" [file]</code></td><td>Prints all lines containing uppercase letters.</td></tr><tr><td><code>grep "[[:lower:]]" [file]</code></td><td>Prints all lines containing lowercase letters.</td></tr></tbody></table>

The character proceeding the {4} must be matched ATLEAST 4 times in a row.

It is looking for "string1111" OR "string1111111111"

Stop reading after finding 4 string pattern matches

```bash
grep "string1\{4\}" [file]
```

The character proceeding the {3,4} must be matched ATLEAST 3 or 4 times in a row.

Looking for "string111", "string1111", OR "string11111111"

```bash
grep "string1\{3,4\}" [file]
```

The character proceeding the {3,} must be matched 3 or more times along with the string pattern

```bash
grep "string1\{3,\}" [file]
```

Strings that have an 'a' and a 'z' seperated by two letters (represented by the dots):

```bash
grep "a..z" [file]
```

Strings that have 'c' and any number of 't's in the pattern:

```bash
grep "c\?t" [file]
```

## <mark style="color:red;">Range</mark>

Extracts a range of lines from the first pattern to the second pattern.

```bash
sed -n '/<pattern>/,/<pattern2>/p' filename
```

## <mark style="color:red;">Before / After Match</mark>

| `grep -B 4 "string" [file]` | Print 4 lines BEFORE string match           |
| --------------------------- | ------------------------------------------- |
| `grep -A 4 "string" [file]` | Print 4 lines AFTER string match            |
| `grep -C 4 "string" [file]` | Print 4 lines BEFORE and AFTER string match |

5 lines before, 10 lines after grep matches

```bash
find .-type f -name "\*.scala"-exec grep -B5 -A10 'null'{} \\;
```

## <mark style="color:red;">Inverse Matches</mark>

<table data-header-hidden><thead><tr><th width="326">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>grep -v "string" [file]</code></td><td>Print all lines that DO NOT contain the string pattern</td></tr><tr><td><code>awk '!/pattern/' filename</code></td><td>Prints lines that do not match the specified pattern</td></tr></tbody></table>

## <mark style="color:red;">Line Numbers</mark>

| `grep -n "string" [file]`                      | Line number as well as the string pattern match        |
| ---------------------------------------------- | ------------------------------------------------------ |
| `sed -n p [file]`                              | Prints by line with line numbers (starts at 1).        |
| `sed -n '2,4p' [file]`                         | Prints lines 2-4.                                      |
| `sed '2,4d' [file]`                            | Excludes lines 2-4.                                    |
| `sed -n -e '2,3p' -e '5,6p' [file]`            | Print multiple sets of lines.                          |
| `awk '{print NR, $0}' [file]`                  | Prints line numbers followed by the entire line.       |
| `awk 'NR>=10 && NR<=20 {print $1, $3}' [file]` | Prints the first and third columns for lines 10 to 20. |

## <mark style="color:red;">Unique / Deduplicate Lines</mark>

Extracts matching lines, sorts them, and filters out duplicates:

```bash
grep "[pattern]" filename | sort | uniq
```

Extract lines that appears once:

```bash
awk '{ seen[$0]++ } END { for (line in seen) if (seen[line] == 1) print line }' text.txt
```

Extracts unique lines that match the pattern using `awk`:

```bash
awk '/cat/ && !seen[$0]++' [file]
```

## <mark style="color:red;">Filter Lines by Length</mark>

Prints lines longer than 80 characters.

```bash
awk 'length($0) > 80' filename
```

## <mark style="color:red;">Use a Source File with Patterns</mark>

Specify a file containing search strings rather than manually supplying each search string.

```bash
grep -f [string file] [file]
```

## <mark style="color:red;">Byte Position</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="411">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>cut -b 1-10 file.bin</code></td><td>Cutting by Byte Position on each line</td></tr><tr><td><code>echo 'Hello, World!' | cut -b 1,7-12</code></td><td>Displaying Specific Bytes from the input string</td></tr></tbody></table>

## <mark style="color:red;">Dates</mark>

Extracts date components and formats them as YYYY-MM-DD.&#x20;

```bash
awk '{split($4,a,"/"); print a[3] "-" a[1] "-" a[2]}' filename
```

## <mark style="color:red;">Unique Elements</mark>

### <mark style="color:purple;">Unique Lines</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="308">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>sort -u [file]</code></td><td>Prints each unique line once, no matter if it appears only 1 time or 100 times.</td></tr><tr><td><code>uniq -u [file]</code></td><td>Prints ONLY lines that appear 1 time. If a line appears more than once it is not printed at all.</td></tr><tr><td><code>sort file | uniq</code></td><td>Sort the file and use <code>uniq</code> to filter out repeated lines. Only adjacent duplicates are removed, so sorting is essential.</td></tr><tr><td><code>sort file | uniq -u</code></td><td>Display only unique lines, eliminating lines that appear more than once.</td></tr><tr><td><code>awk '!seen[$0]++' [file]</code></td><td>Use an associative array <code>seen</code> to track lines. If a line hasn't been seen, print it. This approach doesn't require sorting and keeps the original order.</td></tr></tbody></table>

### <mark style="color:purple;">Unique Words or Elements</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>tr ' ' '\n' &#x3C; file | sort | uniq</code></td><td>Convert spaces to newlines to treat each word as a line, then sort and use <code>uniq</code> to find unique words.</td></tr><tr><td><code>tr ' ' '\n' &#x3C; file | sort | uniq -u</code></td><td>Similar to above, but display words that appear exactly once.</td></tr><tr><td><code>awk '{for(i=1; i&#x3C;=NF; i++) if (!seen[$i]++) print $i}' file</code></td><td>Iterate over every word in each line, track occurrences with an array <code>seen</code>, and print words that appear for the first time.</td></tr></tbody></table>

### <mark style="color:purple;">Multiple Files</mark>

Sort and merge two files, then display lines unique to either file.

```bash
sort file1 file2 \| uniq -u
```

### <mark style="color:purple;">Columns / Fields</mark>

Displaying Unique words in the first field, delimited by commas.

```bash
cut -f 1 -d ',' data.csv | sort | uniq
```

Prints unique values in the first column along with their counts.

```bash
awk '{count[$1]++} END {for (i in count) print i, count[i]}' filename
```
