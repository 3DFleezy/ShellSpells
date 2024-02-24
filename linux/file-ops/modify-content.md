# Modify Content

Note: `sed -i` will change original file.

## Overwrite

| Command                                                    | Description                                                       |
| ---------------------------------------------------------- | ----------------------------------------------------------------- |
| `cat > file`                                               | Overwrite/create file                                             |
| `echo "text" > [file]`                                     | Overwrite/create file                                             |
| `echo "text" \| tee [file]`                                | Overwrite/create file and display                                 |
| `printf "Line 1\nLine 2" > [file]`                         | Overwrite/create file with newlines.                              |
| `awk -v text="some text" 'BEGIN{print text > "filename"}'` | Overwrite/create file                                             |
| `echo "text" \| dd of=file`                                | Write "text" to `file` using `dd`, overwriting existing contents. |

## Insert

### Strings

| Command                                                    | Description                                      |
| ---------------------------------------------------------- | ------------------------------------------------ |
| `echo "text" >> [file]`                                    | Append "text" to the end of a file.              |
| `sed i\text`                                               | Before each line                                 |
| `sed a\text`                                               | After each line                                  |
| `sed '$ a\text' [file]`                                    | Use `sed` to insert "text" at the end of a file. |
| `sed '$a text' file`                                       | Append "text" at the end of `file`.              |
| `sed '1i text' file`                                       | Insert "text" at the beginning of `file`         |
| `awk 'END {print "text"} 1' file > temp && mv temp [file]` | Append "text" at the end of a file.              |

### Lines

| Command                                            | Description                                  |
| -------------------------------------------------- | -------------------------------------------- |
| `sed '1i\New line' [file]`                         | Insert newline at beginning                  |
| `sed '$a\New line' [file]`                         | Append new line at the end                   |
| `sed '/pattern/a\new line' file`                   | Append new line after lines with pattern     |
| `sed G [file]`                                     | Adds blank line between lines (Double Space) |
| `nl -ba file > temp && mv temp file`               | Add line numbers to each line.               |
| `awk '{print NR, $0}' file > temp && mv temp file` | Add line numbers to each line.               |

### Append

| Command                                                | Description                                     |
| ------------------------------------------------------ | ----------------------------------------------- |
| `cat >> file`                                          | Append to `file` from stdin until EOF (Ctrl+D). |
| `echo "text" \| tee -a [file]`                         | Append and display                              |
| `printf "text" >> [file]`                              | Append                                          |
| `awk -v text="more text" '{print $0 ORS text}' [file]` | Append?                                         |

## Replace / Remove

### Replace Strings

| Command                               | Description                                  |
| ------------------------------------- | -------------------------------------------- |
| `sed 's/pattern/new/' [file]`         | Replace pattern with new in file.txt         |
| `sed 's/pattern/new/g' [file]`        | Replace all occurrences of "old" with "new". |
| `sed 's/pattern/new/2' [file]`        | Replace 2nd pattern in a line.               |
| `sed '2 s/pattern/new/' [file]`       | Replace pattern on line 2                    |
| `sed 1,5s/pattern/new/ [file]`        | Replace pattern on lines 1 to 5              |
| `sed /pattern/, /pattern2/s/old/new/` | Replace between two patterns                 |
| `sed $s/pattern/new/`                 | Replace pattern on last line                 |
| `sed 's/,/\n/g' file`                 | Replace Commas with Newline                  |
| `tr , '\n' < file`                    | Replace Commas with Newline                  |

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

### Remove Strings

| Command                    | Description                          |
| -------------------------- | ------------------------------------ |
| `cut -f 1 -d $'\t' [file]` | Suppressing Non-Printable Characters |

### Remove Lines

#### Patterns

| Command                                         | Description                                                  |
| ----------------------------------------------- | ------------------------------------------------------------ |
| `sed '/pattern/d' file`                         | Remove lines matching "pattern".                             |
| `awk '!/pattern/' file > temp && mv temp file`  | Remove lines matching "pattern".                             |
| `grep -v "pattern" file > temp && mv temp file` | Use `grep` with `-v` to filter out lines matching "pattern". |

#### Line Numbers

| Command              | Description                  |
| -------------------- | ---------------------------- |
| `sed '/^9/d' [file]` | Delete lines starting with 9 |
| `sed '1,3d' [file]`  | Delete lines 1 to 3          |

#### Blank Lines

| Command                                    | Description                                                                              |
| ------------------------------------------ | ---------------------------------------------------------------------------------------- |
| `sed '/^$/d' [file]`                       | Remove blank lines.                                                                      |
| `sed 'n;d'`                                | Remove blank lines between lines (Double Spaced) (assumes even numbered lines are blank) |
| `awk 'NF' [file] > temp && mv temp [file]` | Remove blank lines, keeping lines with at least one field.                               |

#### Duplicate Lines

| Command                                         | Description                                                              |
| ----------------------------------------------- | ------------------------------------------------------------------------ |
| `awk '!seen[$0]++' file > temp && mv temp file` | Remove duplicate lines, preserving the order.                            |
| `sort -u file > temp && mv temp file`           | Sort the file and remove duplicate lines, may change the original order. |

#### Comment Lines

Removing lines that start with `#`. E ssentially this removes all the comments out of a file. This is good when examining a config file full of comments when you just want to see a certain line. `cat [file] | grep -v ^\# | grep .` sed '/^#/d' \[file]

## Convert Case

| Command                                                    | Description                                |
| ---------------------------------------------------------- | ------------------------------------------ |
| `tr '[:upper:]' '[:lower:]' < file > temp && mv temp file` | Convert all text to lowercase.             |
| `tr '[:lower:]' '[:upper:]' < file > temp && mv temp file` | Convert all text to uppercase.             |
| `awk '{print tolower($0)}' file > temp && mv temp file`    | Convert all text to lowercase using `awk`. |
| `awk '{print toupper($0)}' file > temp && mv temp file`    | Convert all text to uppercase using `awk`. |

## Text Editors

| Command      | Description                                                                                       |
| ------------ | ------------------------------------------------------------------------------------------------- |
| `vim file`   | Open `file` in Vim editor for editing. Save and exit with `:wq`.                                  |
| `nano file`  | Open `file` in Nano editor for editing. Save and exit with `Ctrl+O`, `Ctrl+X`.                    |
| `emacs file` | Open `file` in Emacs editor for editing. Save with `Ctrl+x Ctrl+s` and exit with `Ctrl+x Ctrl+c`. |
