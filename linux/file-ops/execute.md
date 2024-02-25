# Execute

## <mark style="color:red;">Execute</mark>

<table data-header-hidden><thead><tr><th width="272">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>./file</code></mark></td><td>Execute a file located in the current directory. The file must have execute permissions.</td></tr><tr><td><mark style="color:yellow;"><code>sh file</code></mark></td><td>Execute a shell script using the Bourne shell (or compatible shell).</td></tr><tr><td><mark style="color:yellow;"><code>bash file</code></mark></td><td>Execute a script using the Bash shell.</td></tr><tr><td><mark style="color:yellow;"><code>zsh file</code></mark></td><td>Execute a script using the Zsh shell.</td></tr><tr><td><mark style="color:yellow;"><code>csh file</code></mark></td><td>Execute a script using the C shell.</td></tr><tr><td><mark style="color:yellow;"><code>python [filename]</code></mark></td><td>Executes the script using the Python interpreter (if it's a Python script).</td></tr><tr><td><mark style="color:yellow;"><code>source file</code></mark></td><td>Read and execute commands from <mark style="color:yellow;"><code>file</code></mark> in the current shell environment.</td></tr><tr><td><mark style="color:yellow;"><code>. file</code></mark></td><td>Equivalent to <mark style="color:yellow;"><code>source</code></mark>, reads and executes commands from <mark style="color:yellow;"><code>file</code></mark> in the current shell.</td></tr><tr><td><mark style="color:yellow;"><code>exec file</code></mark></td><td>Replace the current shell with <mark style="color:yellow;"><code>file</code></mark>. The file must be executable.</td></tr><tr><td><mark style="color:yellow;"><code>nohup ./file &#x26;</code></mark></td><td>Execute a file in the background, immune to logout. Useful for long-running processes.</td></tr><tr><td><mark style="color:yellow;"><code>xdg-open [filename]</code></mark></td><td>Opens the file with the appropriate application based on its type (images, documents, etc.).</td></tr></tbody></table>

### <mark style="color:purple;">at</mark>

Schedule <mark style="color:yellow;">`file`</mark> for execution 5 minutes from now. <mark style="color:yellow;">`atd`</mark> service must be running:

```bash
echo "./file" | at now + 5 minutes
```

### <mark style="color:purple;">Cron</mark>

Add a cron job by editing the crontab with <mark style="color:yellow;">`crontab -e`</mark>, then add a line according to the desired schedule:

<mark style="color:yellow;">`* * * * * /path/to/file`</mark>
