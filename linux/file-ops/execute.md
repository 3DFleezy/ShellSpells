# Execute

## Execute

| Command               | Description                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------------- |
| `./file`              | Execute a file located in the current directory. The file must have execute permissions.     |
| `sh file`             | Execute a shell script using the Bourne shell (or compatible shell).                         |
| `bash file`           | Execute a script using the Bash shell.                                                       |
| `zsh file`            | Execute a script using the Zsh shell.                                                        |
| `csh file`            | Execute a script using the C shell.                                                          |
| `python [filename]`   | Executes the script using the Python interpreter (if it's a Python script).                  |
| `source file`         | Read and execute commands from `file` in the current shell environment.                      |
| `. file`              | Equivalent to `source`, reads and executes commands from `file` in the current shell.        |
| `exec file`           | Replace the current shell with `file`. The file must be executable.                          |
| `nohup ./file &`      | Execute a file in the background, immune to logout. Useful for long-running processes.       |
| `xdg-open [filename]` | Opens the file with the appropriate application based on its type (images, documents, etc.). |

### at

Schedule `file` for execution 5 minutes from now. `atd` service must be running:

`echo "./file" | at now + 5 minutes`

### Cron

Add a cron job by editing the crontab with `crontab -e`, then add a line according to the desired schedule:

`* * * * * /path/to/file`
