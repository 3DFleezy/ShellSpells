# Working With Weird Filenames

## Quoting

Single quotes: Prevent interpretation special characters within the quotes.

Double quotes: Allow interpretation of variables, backticks, and the escape character ().

```bash
cat 'filename with spaces.txt'
cat "another file with spaces and $variable.txt"
```

## Escaping

Use a backslash `\` to escape spaces and special characters in filenames.

```bash
cat filename\ with\ spaces.txt
```

## Using find with -print0 and xargs -0

The `find` command's `-print0` option prints the full file name on the standard output, followed by a null character.

This can be piped into `xargs -0` for safe parsing of filenames with special characters:

```bash
find . -type f -print0 | xargs -0 command
```

## Looping Over Files with Shell Globbing

When dealing with files directly in shell scripts or command lines, use shell loops and globbing, ensuring to quote the variable that holds the filename:

```bash
for file in *; do
  command "$file"
done
```

## Using find with -exec

The `-exec` option of find directly executes a command on each found file, correctly handling filenames with special characters without needing pipes or xargs:

```bash
find . -type f -exec command '{}' \;
```

## Using the -- Indicator

Many Unix commands support `--` to indicate the end of command options.

After `--`, anything is treated as a filename, even if it starts with `-`.

```bash
rm -- -filename-starting-with-hyphen.txt
```

Interacting with files that start with a `-`

Moving a file called: -MoveMe.txt in to a dir called `- folder`

```bash
mv -- -MoveMe.txt '''- folder'''
```
