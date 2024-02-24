# History

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Commands</mark>

| Command                         | Description                                                                                    |
| ------------------------------- | ---------------------------------------------------------------------------------------------- |
| `history`                       | Earlier commands used by the user.                                                             |
| `history \| grep <search_term>` | Searches for specific commands in the history                                                  |
| `history \| less`               | Paginates through the command history                                                          |
| `history \| tail`               | Displays the most recent commands in the history                                               |
| `fc -l`                         | Lists, edits, or re-executes commands from the history list                                    |
| `cat ~/.bash_history`           | Displays the entire command history                                                            |
| `cat ~/.*history \| less`       | View history                                                                                   |
| `env`                           | Run this first because you want to see A) If the HISTFILE is set B) What env variables are set |
| `printenv`                      | Similar to `env`, shows environment variables                                                  |

### <mark style="color:purple;">Find History Files</mark>

| Command                      | Description                                                                               |
| ---------------------------- | ----------------------------------------------------------------------------------------- |
| `find / -name .bash_history` | Searches for bash history files for all users.                                            |
| `find / -name .zsh_history`  | Locates Zsh history files across the filesystem.                                          |
| `find / -name .history`      | Finds generic shell history files, applicable to various shells.                          |
| `ls -la ~/.*_history`        | Lists all history files in the current user's home directory, covering bash, zsh, etc.    |
| `echo $HISTFILE`             | Displays the path to the current shell's history file, works in shells like bash and zsh. |

### <mark style="color:purple;">Find Creds in History Files</mark>

| Command                                  | Description                                                                       |
| ---------------------------------------- | --------------------------------------------------------------------------------- |
| `history \| grep -i password`            | Searches command history for the term "password"                                  |
| `history \| grep -i "api_key"`           | Looks for occurrences of "api\_key" in command history                            |
| `history \| grep -i "secret"`            | Filters command history for the term "secret"                                     |
| `history \| grep -E "pass\|key\|secret"` | Uses extended regex to search for multiple terms related to sensitive information |



## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">Unset History</mark>

| Command                                 | Description                                   |
| --------------------------------------- | --------------------------------------------- |
| `\unset HISTFILE HISTSIZE HISTFILESIZE` | Removes the history of your current commands. |

### <mark style="color:purple;">Bash</mark>

| Command               | Description                                                      |
| --------------------- | ---------------------------------------------------------------- |
| `history -d <number>` | Deletes specific entries from your history.                      |
| `history -c`          | Clears your entire history.                                      |
| `history -a`          | Appends history to a file (e.g., history -a \~/my\_history.log). |

### <mark style="color:purple;">Zsh</mark>

| Command             | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| `history -g`        | Shows global history across sessions.                       |
| `history -d oldest` | Deletes the oldest entry.                                   |
| `history -f`        | Saves history to a file (e.g., history -f \~/zsh\_history). |

