# Extract Content

## Basic Pattern Match

| Command                         | Description                                                                                 |
| ------------------------------- | ------------------------------------------------------------------------------------------- |
| `cat [file] \| grep "string"`   | Lines with match                                                                            |
| `sed /pattern/ [file]`          | Lines with match                                                                            |
| `sed -n '/[pattern]/p' [file]`  | Lines with match                                                                            |
| `awk '/[pattern]/' [file]`      | Lines with match                                                                            |
| `grep "string" [file]`          | Lines with match                                                                            |
| `grep -i "string" [file]`       | Case insensitive                                                                            |
| `grep -E "<regex>" [file]`      | Uses extended regular expressions for pattern matching.                                     |
| `grep -w "string" [file]`       | Print all lines with the whole word matching the string pattern.                            |
| `grep "\\bstring\\b" [file]`    | Print all lines with string pattern match with a space before or after.                     |
| `grep "string1?" [file]`        | ? = optional. Prints lines that match at least 1 time                                       |
| `grep "string1\*" [file]`       | The character proceeding the "\*" is optional                                               |
| `grep "string1+" [file]`        | The character proceeding the "+" is optional. Optional character must match at least 1 time |
| `grep -P "<perl_regex>" [file]` | Uses Perl-compatible regular expressions for pattern matching (if supported by `grep`).     |

## Exact Line Match

| Command                        | Description                                |
| ------------------------------ | ------------------------------------------ |
| `grep -x "entire line" [file]` | Lines that exactly match the whole pattern |

## Strings (Not lines)

| Command                                             | Description                                                                                |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| `grep -o "pattern" [file]`                          | Extract and print only the parts of a line that match the "pattern".                       |
| `egrep -o "pattern" [file]`                         | Similar to `grep -o`, but supports extended regular expressions for more complex patterns. |
| `sed -n 's/.*pattern\(.*\)/\1/p' [file]`            | Extract and print text following "pattern".                                                |
| `cut -d':' -f1 [file]`                              | Extract and print the first field from lines, assuming ':' delimiter.                      |
| `sed -n 's/.*pattern\(.*\)/\1/p' [file]`            | Extract and print text following "pattern".                                                |
| `perl -ne 'print "$1\n" if /.*pattern(.*)/' [file]` | Extract and print text following "pattern".                                                |

## Start/End of Line

| Command                 | Description              |
| ----------------------- | ------------------------ |
| `grep "^string" [file]` | Start with pattern match |
| `sed /^pattern/ [file]` | Start with pattern match |
| `grep "string$" [file]` | End with pattern match   |
| `sed /pattern$/ [file]` | End with pattern match   |

## Columns/Fields

| Command                            | Description                                                          |
| ---------------------------------- | -------------------------------------------------------------------- |
| `awk '{print $1, $3}' [file]`      | Prints the first and third columns of each line in the file          |
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

### Delimiters

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

### Calculate Sum of Column

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

### Print Rows with Max Value in a Column

Identifies and prints the row with the maximum value in the third column.

```bash
awk '{if ($3 > max) {max=$3; row=$0}} END {print row}' filename
```

### Format Column Width

```bash
awk '{printf "%-10s %-8s\n", $1, $2}' filename `| Formats and prints the first two columns with specific width.
```

## Limit Matches

Stop reading after finding 4 string pattern matches:

```bash
grep -m 4 "string" [file]
```

## Multiple Patterns

| Command                                              | Description                                              |
| ---------------------------------------------------- | -------------------------------------------------------- |
| `grep -E "string1\|string2\|string3" [file]`         | Search for 2 or more pattern matches using extended grep |
| `egrep "pattern1\|pattern2\|pattern3" [file]`        | Search for 2 or more pattern matches using extended grep |
| `grep -e "string1" -e "string2" -e "string3" [file]` | Search for 2 or more pattern matches.                    |
| `sed /pattern1/p; /pattern2/p [file]`                | Search for 2 separate pattern matches using sed.         |

## Characters

| Command                                                                   | Description                                             |
| ------------------------------------------------------------------------- | ------------------------------------------------------- |
| `cut -c1-10 [file]`                                                       | Extracts the first 10 characters of each line.          |
| `awk '{print substr($0, 1, 10)}' [file]`                                  | Extracts the first 10 characters of each line.          |
| `cut -c5,7,9 [file]`                                                      | Extracts the 5th, 7th, and 9th characters of each line. |
| `awk '{print substr($0, 5, 1) substr($0, 7, 1) substr($0, 9, 1)}' [file]` | Extracts the 5th, 7th, and 9th characters of each line. |
| `awk '{print substr($0, length($0), 1)}' [file]`                          | Extracts the last character of each line.               |
| `sed 's/.*\(.\)$/\1/' [file]`                                             | Extracts the last character of each line.               |
| `grep "[[:digit:]]" [file]`                                               | Prints all lines containing digits.                     |
| `grep "[[:upper:]]" [file]`                                               | Prints all lines containing uppercase letters.          |
| `grep "[[:lower:]]" [file]`                                               | Prints all lines containing lowercase letters.          |

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

## Range

| Command                                        | Description                                                             |
| ---------------------------------------------- | ----------------------------------------------------------------------- |
| `sed -n '/<pattern1>/,/<pattern2>/p' filename` | Extracts a range of lines from the first pattern to the second pattern. |

## Before / After Match

| Command                     | Description                                 |
| --------------------------- | ------------------------------------------- |
| `grep -B 4 "string" [file]` | Print 4 lines BEFORE string match           |
| `grep -A 4 "string" [file]` | Print 4 lines AFTER string match            |
| `grep -C 4 "string" [file]` | Print 4 lines BEFORE and AFTER string match |

5 lines before, 10 lines after grep matches

```bash
find .-type f -name "\*.scala"-exec grep -B5 -A10 'null'{} \\;
```

## Inverse Matches

| Command                     | Description                                            |
| --------------------------- | ------------------------------------------------------ |
| `grep -v "string" [file]`   | Print all lines that DO NOT contain the string pattern |
| `awk '!/pattern/' filename` | Prints lines that do not match the specified pattern   |

## Line Numbers

| Command                                        | Description                                            |
| ---------------------------------------------- | ------------------------------------------------------ |
| `grep -n "string" [file]`                      | Line number as well as the string pattern match        |
| `sed -n p [file]`                              | Prints by line with line numbers (starts at 1).        |
| `sed -n '2,4p' [file]`                         | Prints lines 2-4.                                      |
| `sed '2,4d' [file]`                            | Excludes lines 2-4.                                    |
| `sed -n -e '2,3p' -e '5,6p' [file]`            | Print multiple sets of lines.                          |
| `awk '{print NR, $0}' [file]`                  | Prints line numbers followed by the entire line.       |
| `awk 'NR>=10 && NR<=20 {print $1, $3}' [file]` | Prints the first and third columns for lines 10 to 20. |

## Unique / Deduplicate Lines

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

## Filter Lines by Length

| Command                          | Description                             |
| -------------------------------- | --------------------------------------- |
| `awk 'length($0) > 80' filename` | Prints lines longer than 80 characters. |

## Use a Source File with Patterns

| Command                        | Description                                                             |
| ------------------------------ | ----------------------------------------------------------------------- |
| `grep -f [string file] [file]` | Specify a file containing search strings for searching in another file. |

## Byte Position

| Command                                 | Description                                     |
| --------------------------------------- | ----------------------------------------------- |
| `cut -b 1-10 file.bin`                  | Cutting by Byte Position on each line           |
| `echo 'Hello, World!' \| cut -b 1,7-12` | Displaying Specific Bytes from the input string |

## Dates

Extracts date components and formats them as YYYY-MM-DD. \` awk '{split($4,a,"/"); print a\[3] "-" a\[1] "-" a\[2]}' filename

## Unique Elements

### Unique Lines

| Command                    | Description                                                                                                                                               |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sort -u [file]`           | Prints each unique line once, no matter if it appears only 1 time or 100 times.                                                                           |
| `uniq -u [file]`           | Prints ONLY lines that appear 1 time. If a line appears more than once it is not printed at all.                                                          |
| `sort file \| uniq`        | Sort the file and use `uniq` to filter out repeated lines. Only adjacent duplicates are removed, so sorting is essential.                                 |
| `sort file \| uniq -u`     | Display only unique lines, eliminating lines that appear more than once.                                                                                  |
| `awk '!seen[$0]++' [file]` | Use an associative array `seen` to track lines. If a line hasn't been seen, print it. This approach doesn't require sorting and keeps the original order. |

### Unique Words or Elements

| Command                                                       | Description                                                                                                                   |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `tr ' ' '\n' < file \| sort \| uniq`                          | Convert spaces to newlines to treat each word as a line, then sort and use `uniq` to find unique words.                       |
| `tr ' ' '\n' < file \| sort \| uniq -u`                       | Similar to above, but display words that appear exactly once.                                                                 |
| `awk '{for(i=1; i<=NF; i++) if (!seen[$i]++) print $i}' file` | Iterate over every word in each line, track occurrences with an array `seen`, and print words that appear for the first time. |

### Multiple Files

Sort and merge two files, then display lines unique to either file.

```bash
sort file1 file2 \| uniq -u
```

### Columns / Fields

Displaying Unique words in the first field, delimited by commas.

```bash
cut -f 1 -d ',' data.csv | sort | uniq
```

Prints unique values in the first column along with their counts.

```bash
awk '{count[$1]++} END {for (i in count) print i, count[i]}' filename
```
