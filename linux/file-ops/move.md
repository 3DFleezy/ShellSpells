# Move

| Command                    | Description                                                                                    |
| -------------------------- | ---------------------------------------------------------------------------------------------- |
| `mv [file] /put/file/here` | Move file.                                                                                     |
| `mv file1 file2 /dir`      | Move multiple files.                                                                           |
| `mv * /dir`                | Move all files in the current directory to `/dir`.                                             |
| `mv *.txt /dir`            | Move all `.txt` files in the current directory to `/dir`.                                      |
| `mv .[^.]* /dir`           | Move all hidden files (those starting with a dot) to `/dir`. This pattern avoids `.` and `..`. |
| `mv -v [file] /dir`        | Verbose output, showing the file names as they are moved.                                      |
| `mv -n [file] /dir`        | No Clobber. Won't overwriting any existing file in the target location.                        |
