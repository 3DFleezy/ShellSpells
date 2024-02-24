# History

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Commands</mark>

<table data-header-hidden><thead><tr><th width="280">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>history</code></mark></td><td>Earlier commands used by the user.</td></tr><tr><td><mark style="color:yellow;"><code>history | grep &#x3C;search_term></code></mark></td><td>Searches for specific commands in the history.</td></tr><tr><td><mark style="color:yellow;"><code>history | less</code></mark></td><td>Paginates through the command history.</td></tr><tr><td><mark style="color:yellow;"><code>history | tail</code></mark></td><td>Displays the most recent commands in the history.</td></tr><tr><td><mark style="color:yellow;"><code>fc -l</code></mark></td><td>Lists, edits, or re-executes commands from the history list.</td></tr><tr><td><mark style="color:yellow;"><code>cat ~/.bash_history</code></mark></td><td>Displays the entire command history.</td></tr><tr><td><mark style="color:yellow;"><code>cat ~/.*history | less</code></mark></td><td>View history</td></tr><tr><td><mark style="color:yellow;"><code>env</code></mark></td><td>Run this first because you want to see A) If the HISTFILE is set B) What env variables are set.</td></tr><tr><td><mark style="color:yellow;"><code>printenv</code></mark></td><td>Similar to <mark style="color:yellow;"><code>env</code></mark>, shows environment variables. can be leveraged.</td></tr></tbody></table>

### <mark style="color:purple;">Find History Files</mark>

<table data-header-hidden><thead><tr><th width="310">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -name .bash_history</code></mark></td><td>Searches for bash history files for all users.</td></tr><tr><td><mark style="color:yellow;"><code>find / -name .zsh_history</code></mark></td><td>Locates Zsh history files across the filesystem.</td></tr><tr><td><mark style="color:yellow;"><code>find / -name .history</code></mark></td><td>Finds generic shell history files, applicable to various shells.</td></tr><tr><td><mark style="color:yellow;"><code>ls -la ~/.*_history</code></mark></td><td>Lists all history files in the current user's home directory, covering bash, zsh, etc.</td></tr><tr><td><mark style="color:yellow;"><code>echo $HISTFILE</code></mark></td><td>Displays the path to the current shell's history file, works in shells like bash and zsh.</td></tr></tbody></table>

### <mark style="color:purple;">Find Creds in History Files</mark>

| <mark style="color:yellow;">`history \| grep -i password`</mark>            | Searches command history for the term "password".                                  |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| <mark style="color:yellow;">`history \| grep -i "api_key"`</mark>           | Looks for occurrences of "api\_key" in command history.                            |
| <mark style="color:yellow;">`history \| grep -i "secret"`</mark>            | Filters command history for the term "secret".                                     |
| <mark style="color:yellow;">`history \| grep -E "pass\|key\|secret"`</mark> | Uses extended regex to search for multiple terms related to sensitive information. |

## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">Unset History</mark>

Removes the history of your current commands:

```bash
\unset HISTFILE HISTSIZE HISTFILESIZE
```

### <mark style="color:purple;">Bash</mark>

<table data-header-hidden><thead><tr><th width="285">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>history -d &#x3C;number></code></mark></td><td>Deletes specific entries from your history.</td></tr><tr><td><mark style="color:yellow;"><code>history -c</code></mark></td><td>Clears your entire history.</td></tr><tr><td><mark style="color:yellow;"><code>history -a</code></mark></td><td>Appends history to a file (e.g., history -a ~/my_history.log).</td></tr></tbody></table>

### <mark style="color:purple;">Zsh</mark>

<table data-header-hidden><thead><tr><th width="282">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>history -g</code></mark></td><td>Shows global history across sessions.</td></tr><tr><td><mark style="color:yellow;"><code>history -d oldest</code></mark></td><td>Deletes the oldest entry.</td></tr><tr><td><mark style="color:yellow;"><code>history -f</code></mark></td><td>Saves history to a file (e.g., history -f ~/zsh_history).</td></tr></tbody></table>
