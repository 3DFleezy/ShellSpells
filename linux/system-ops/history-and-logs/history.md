# History

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Commands</mark>

<table data-header-hidden><thead><tr><th width="280">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>history</code></td><td>Earlier commands used by the user.</td></tr><tr><td><code>history | grep &#x3C;search_term></code></td><td>Searches for specific commands in the history.</td></tr><tr><td><code>history | less</code></td><td>Paginates through the command history.</td></tr><tr><td><code>history | tail</code></td><td>Displays the most recent commands in the history.</td></tr><tr><td><code>fc -l</code></td><td>Lists, edits, or re-executes commands from the history list.</td></tr><tr><td><code>cat ~/.bash_history</code></td><td>Displays the entire command history.</td></tr><tr><td><code>cat ~/.*history | less</code></td><td>View history</td></tr><tr><td><code>env</code></td><td>Run this first because you want to see A) If the HISTFILE is set B) What env variables are set.</td></tr><tr><td><code>printenv</code></td><td>Similar to <code>env</code>, shows environment variables. can be leveraged.</td></tr></tbody></table>

### <mark style="color:purple;">Find History Files</mark>

<table data-header-hidden><thead><tr><th width="310">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>find / -name .bash_history</code></td><td>Searches for bash history files for all users.</td></tr><tr><td><code>find / -name .zsh_history</code></td><td>Locates Zsh history files across the filesystem.</td></tr><tr><td><code>find / -name .history</code></td><td>Finds generic shell history files, applicable to various shells.</td></tr><tr><td><code>ls -la ~/.*_history</code></td><td>Lists all history files in the current user's home directory, covering bash, zsh, etc.</td></tr><tr><td><code>echo $HISTFILE</code></td><td>Displays the path to the current shell's history file, works in shells like bash and zsh.</td></tr></tbody></table>

### <mark style="color:purple;">Find Creds in History Files</mark>

| Command                                  | Description                                                                        |
| ---------------------------------------- | ---------------------------------------------------------------------------------- |
| `history \| grep -i password`            | Searches command history for the term "password".                                  |
| `history \| grep -i "api_key"`           | Looks for occurrences of "api\_key" in command history.                            |
| `history \| grep -i "secret"`            | Filters command history for the term "secret".                                     |
| `history \| grep -E "pass\|key\|secret"` | Uses extended regex to search for multiple terms related to sensitive information. |



## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">Unset History</mark>

Removes the history of your current commands:

```bash
\unset HISTFILE HISTSIZE HISTFILESIZE
```

### <mark style="color:purple;">Bash</mark>

<table><thead><tr><th width="285">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>history -d &#x3C;number></code></td><td>Deletes specific entries from your history.</td></tr><tr><td><code>history -c</code></td><td>Clears your entire history.</td></tr><tr><td><code>history -a</code></td><td>Appends history to a file (e.g., history -a ~/my_history.log).</td></tr></tbody></table>

### <mark style="color:purple;">Zsh</mark>

<table><thead><tr><th width="282">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>history -g</code></td><td>Shows global history across sessions.</td></tr><tr><td><code>history -d oldest</code></td><td>Deletes the oldest entry.</td></tr><tr><td><code>history -f</code></td><td>Saves history to a file (e.g., history -f ~/zsh_history).</td></tr></tbody></table>

