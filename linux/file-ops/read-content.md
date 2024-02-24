# Read Content

| Command                     | Description                                                                          |
| --------------------------- | ------------------------------------------------------------------------------------ |
| `cat [file]`                | Display all                                                                          |
| `less [file]`               | Paging with search                                                                   |
| `more [file]`               | Paging                                                                               |
| `head [file]`               | First lines (default is 10 lines)                                                    |
| `head -n 15 [file]`         | First 15 lines.                                                                      |
| `tail [file]`               | Last lines (default is 10 lines)                                                     |
| `tail -n 15 [file]`         | Last 15 lines.                                                                       |
| `tail -f [file]`            | Continuously monitor for new lines, useful for logs.                                 |
| `nl [file]`                 | Display contents with line numbers                                                   |
| `od -c [file]`              | Display in octal along with ASCII characters.                                        |
| `hexdump -C [file]`         | Display in hex. Useful for binaries.                                                 |
| `strings [file]`            | Extract and display printable strings.                                               |
| `zcat file.gz`              | Display contents of gzipped files without decompressing it on disk.                  |
| `zless file.gz`             | View the contents of a gzipped \[file] in an interactive `less`-like interface.      |
| `zmore file.gz`             | View the contents of a gzipped \[file] page by page, similar to `more`.              |
| `bzcat file.bz2`            | Display the contents of a bzip2-compressed \[file] without decompressing it on disk. |
| `highlight --syntax [file]` | Applies syntax highlighting based on the file type.                                  |
