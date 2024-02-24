# History

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Commands</mark>

| `history`                       | Earlier commands used by the user.                                                             |
| ------------------------------- | ---------------------------------------------------------------------------------------------- |
| `history \| grep <search_term>` | Searches for specific commands in the history                                                  |
| `history \| less`               | Paginates through the command history                                                          |
| `history \| tail`               | Displays the most recent commands in the history                                               |
| `fc -l`                         | Lists, edits, or re-executes commands from the history list                                    |
| `cat ~/.bash_history`           | Displays the entire command history                                                            |
| `cat ~/.*history \| less`       | View history                                                                                   |
| `env`                           | Run this first because you want to see A) If the HISTFILE is set B) What env variables are set |
| `printenv`                      | Similar to `env`, shows environment variables                                                  |

### <mark style="color:purple;">Find History Files</mark>

| `find / -name .bash_history` | Searches for bash history files for all users.                                            |
| ---------------------------- | ----------------------------------------------------------------------------------------- |
| `find / -name .zsh_history`  | Locates Zsh history files across the filesystem.                                          |
| `find / -name .history`      | Finds generic shell history files, applicable to various shells.                          |
| `ls -la ~/.*_history`        | Lists all history files in the current user's home directory, covering bash, zsh, etc.    |
| `echo $HISTFILE`             | Displays the path to the current shell's history file, works in shells like bash and zsh. |

### <mark style="color:purple;">Find Creds in History Files</mark>

| `history \| grep -i password`            | Searches command history for the term "password"                                  |
| ---------------------------------------- | --------------------------------------------------------------------------------- |
| `history \| grep -i "api_key"`           | Looks for occurrences of "api\_key" in command history                            |
| `history \| grep -i "secret"`            | Filters command history for the term "secret"                                     |
| `history \| grep -E "pass\|key\|secret"` | Uses extended regex to search for multiple terms related to sensitive information |



## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">Unset History</mark>

<table><thead><tr><th width="423">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>\unset HISTFILE HISTSIZE HISTFILESIZE</code></td><td>Removes the history of your current commands.</td></tr></tbody></table>

### <mark style="color:purple;">Bash</mark>

<table><thead><tr><th width="285">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>history -d &#x3C;number></code></td><td>Deletes specific entries from your history.</td></tr><tr><td><code>history -c</code></td><td>Clears your entire history.</td></tr><tr><td><code>history -a</code></td><td>Appends history to a file (e.g., history -a ~/my_history.log).</td></tr></tbody></table>

### <mark style="color:purple;">Zsh</mark>

<table><thead><tr><th width="282">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>history -g</code></td><td>Shows global history across sessions.</td></tr><tr><td><code>history -d oldest</code></td><td>Deletes the oldest entry.</td></tr><tr><td><code>history -f</code></td><td>Saves history to a file (e.g., history -f ~/zsh_history).</td></tr></tbody></table>

