# Compress/Decompress

## Compressing Files

| Command                         | Description                                                                |
| ------------------------------- | -------------------------------------------------------------------------- |
| `gzip file`                     | Compress `file` using gzip.                                                |
| `bzip2 file`                    | Compress `file` using bzip2.                                               |
| `xz file`                       | Compress `file` using xz.                                                  |
| `zip archive.zip file`          | Compress `file` into a zip archive named `archive.zip`.                    |
| `tar -czf archive.tar.gz file`  | Create a gzip-compressed tar archive `archive.tar.gz` containing `file`.   |
| `tar -cjf archive.tar.bz2 file` | Create a bzip2-compressed tar archive `archive.tar.bz2` containing `file`. |
| `tar -cJf archive.tar.xz file`  | Create an xz-compressed tar archive `archive.tar.xz` containing `file`.    |

## Decompressing Files

| Command                    | Description                                                                   |
| -------------------------- | ----------------------------------------------------------------------------- |
| `gunzip file.gz`           | Decompress a gzip-compressed file.                                            |
| `bunzip2 file.bz2`         | Decompress a bzip2-compressed file.                                           |
| `unxz file.xz`             | Decompress an xz-compressed file.                                             |
| `unzip archive.zip`        | Extract files from a zip archive.                                             |
| `tar -xzf archive.tar.gz`  | Extract a gzip-compressed tar archive.                                        |
| `tar -xjf archive.tar.bz2` | Extract a bzip2-compressed tar archive.                                       |
| `tar -xJf archive.tar.xz`  | Extract an xz-compressed tar archive.                                         |
| `tar -xvf [file]`          | Extract files from a tar archive, with verbose output and progress indicator. |
