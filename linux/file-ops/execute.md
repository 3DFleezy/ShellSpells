# Execute

## <mark style="color:red;">Execute</mark>

<table data-header-hidden><thead><tr><th width="272">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>./file</code></td><td>Execute a file located in the current directory. The file must have execute permissions.</td></tr><tr><td><code>sh file</code></td><td>Execute a shell script using the Bourne shell (or compatible shell).</td></tr><tr><td><code>bash file</code></td><td>Execute a script using the Bash shell.</td></tr><tr><td><code>zsh file</code></td><td>Execute a script using the Zsh shell.</td></tr><tr><td><code>csh file</code></td><td>Execute a script using the C shell.</td></tr><tr><td><code>python [filename]</code></td><td>Executes the script using the Python interpreter (if it's a Python script).</td></tr><tr><td><code>source file</code></td><td>Read and execute commands from <code>file</code> in the current shell environment.</td></tr><tr><td><code>. file</code></td><td>Equivalent to <code>source</code>, reads and executes commands from <code>file</code> in the current shell.</td></tr><tr><td><code>exec file</code></td><td>Replace the current shell with <code>file</code>. The file must be executable.</td></tr><tr><td><code>nohup ./file &#x26;</code></td><td>Execute a file in the background, immune to logout. Useful for long-running processes.</td></tr><tr><td><code>xdg-open [filename]</code></td><td>Opens the file with the appropriate application based on its type (images, documents, etc.).</td></tr></tbody></table>

### <mark style="color:purple;">at</mark>

Schedule `file` for execution 5 minutes from now. `atd` service must be running:

`echo "./file" | at now + 5 minutes`

### <mark style="color:purple;">Cron</mark>

Add a cron job by editing the crontab with `crontab -e`, then add a line according to the desired schedule:

`* * * * * /path/to/file`
