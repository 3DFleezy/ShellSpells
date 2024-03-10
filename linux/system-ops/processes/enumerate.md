# Enumerate

## <mark style="color:red;">Process Observation</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="281">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>systemd-cgls</code></mark></td><td>Shows process additional context. Useful for finding malware.</td></tr><tr><td><mark style="color:yellow;"><code>ps -A</code></mark></td><td>View all running processes</td></tr><tr><td><mark style="color:yellow;"><code>ps axjf</code></mark></td><td>Process tree</td></tr><tr><td><mark style="color:yellow;"><code>pstree</code></mark></td><td>Process tree</td></tr><tr><td><mark style="color:yellow;"><code>ps -auxf</code></mark></td><td>Processes including CPU and MEM</td></tr><tr><td><mark style="color:yellow;"><code>ps -efH</code></mark></td><td>Processes using standard syntax with process hierarchy</td></tr><tr><td><mark style="color:yellow;"><code>/proc/version</code></mark></td><td>Info about system processes</td></tr><tr><td><mark style="color:yellow;"><code>lsof</code></mark></td><td>Lists all open files belonging to all active processes</td></tr><tr><td><mark style="color:yellow;"><code>lsof -c &#x3C;command_name></code></mark></td><td>Listing of files for processes executing the command</td></tr><tr><td><mark style="color:yellow;"><code>lsof -i &#x3C;4|6></code></mark></td><td>Only files of the indicated IP version, IPv4 or IPv6</td></tr><tr><td><mark style="color:yellow;"><code>top</code></mark></td><td>Display real-time system statistics</td></tr><tr><td><mark style="color:yellow;"><code>top -u &#x3C;username></code></mark></td><td>User-specific processes</td></tr><tr><td><mark style="color:yellow;"><code>htop</code></mark></td><td>Interactive process viewer (May need install)</td></tr></tbody></table>

### <mark style="color:purple;">Identifying Suspicious Activity</mark>

Network connections: View open network connections and identify processes making unusual connections. Resource usage: Processes consuming excessive resources might be suspicious. File access: Monitor file access to identify processes accessing sensitive files or system locations.

## <mark style="color:red;">PID</mark>

### <mark style="color:purple;">Finding Process PIDs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="440">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>pidof [process_name]</code></mark></td><td>Finds the PIDs of running processes by name</td></tr><tr><td><mark style="color:yellow;"><code>pgrep [process_name]</code></mark></td><td>Finds process IDs for matching processes</td></tr></tbody></table>

### <mark style="color:purple;">Finding Processes by PIDs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="434">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ps -p [PID]</code></mark></td><td>Displays information for a specific process ID.</td></tr><tr><td><mark style="color:yellow;"><code>ps -fp [PID]</code></mark></td><td>Info about a specific process, given its process ID (PID)</td></tr><tr><td><mark style="color:yellow;"><code>pgrep [pattern]</code></mark></td><td>Lists process IDs matching a pattern.</td></tr><tr><td><mark style="color:yellow;"><code>lsof -p [PID]</code></mark></td><td>Lists all open files by PID.</td></tr><tr><td><mark style="color:yellow;"><code>ls -al /proc/[PID]</code></mark></td><td>Shows the PIDs of processes in <mark style="color:yellow;"><code>/proc</code></mark>.</td></tr><tr><td><mark style="color:yellow;"><code>cat /proc/[PID]/maps</code></mark></td><td>Displays the memory mappings of a specific process identified by its process ID (PID).</td></tr><tr><td><mark style="color:yellow;"><code>ls -al /proc/[PID]/fd | grep \\/</code></mark></td><td>Shows only directories</td></tr><tr><td><mark style="color:yellow;"><code>readlink -f /proc/[PID]/exe</code></mark></td><td>Examines running processes</td></tr></tbody></table>

## <mark style="color:red;">Process Name</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="432">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>grep [process_name] /var/log/*</code></mark></td><td>Search through all files in the directory for a file containing [process_name].</td></tr><tr><td><mark style="color:yellow;"><code>tail -f /var/log/messages</code></mark></td><td>Prints the last 10 lines of <mark style="color:yellow;"><code>/var/log/messages</code></mark> and monitors the file for new lines.</td></tr><tr><td><mark style="color:yellow;"><code>find / -name *[process_name]*</code></mark></td><td>Starting in "/", find something containing the phrase [process_name]</td></tr><tr><td><mark style="color:yellow;"><code>chkconfig --list | grep [process_name]</code></mark></td><td>Queries runlevel information for system services</td></tr><tr><td><mark style="color:yellow;"><code>chkconfig --list</code></mark></td><td>Queries runlevel info for system services.</td></tr><tr><td><mark style="color:yellow;"><code>ps -p [PID] -o comm=</code></mark></td><td>Displays the name of the process with the specified PID.</td></tr></tbody></table>

## <mark style="color:red;">Shared Objects</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>lsof -N -n | grep '.so'</code></mark></td><td>Lists open files, including shared objects (libraries) mapped into memory by processes.</td></tr><tr><td><mark style="color:yellow;"><code>find /proc/*/maps -type f -exec grep -H '\.so' {} \;</code></mark></td><td>Inspects processes and their mapped shared objects directly using the proc filesystem.</td></tr><tr><td><mark style="color:yellow;"><code>pmap [PID] | grep '/lib/'</code></mark></td><td>Displays the memory map of a process, including shared objects.</td></tr><tr><td><mark style="color:yellow;"><code>ldd /executable | grep '/lib/'</code></mark></td><td>Lists dynamic dependencies of an executable, including shared objects.</td></tr><tr><td><mark style="color:yellow;"><code>pldd [PID]</code></mark></td><td>Gets shared objects used by that process</td></tr></tbody></table>

Lists processes and filters by shared objects using `awk`:

```bash
ps aux | awk '{print $2}' | xargs -I{} readlink /proc/{}/exe | grep '/lib/'
```

Lists shared objects being used by running processes:

{% code overflow="wrap" %}
```bash
ps aux | awk '{print $2}' | xargs -I{} readlink /proc/{}/exe | xargs lsof -p | grep -E '.so(..+)?$'
```
{% endcode %}

## <mark style="color:red;">User</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="336">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ps aux</code></mark></td><td>Processes for all users</td></tr><tr><td><mark style="color:yellow;"><code>ps -u &#x3C;username></code></mark></td><td>Lists processes running under a specific user.</td></tr><tr><td><mark style="color:yellow;"><code>ps aux | grep euid=&#x3C;-UUID></code></mark></td><td>Find process by user UUID.</td></tr><tr><td><mark style="color:yellow;"><code>ps aux | grep root</code></mark></td><td>Root processes</td></tr><tr><td><mark style="color:yellow;"><code>ps -U UID</code></mark></td><td>Shows processes for a user specified by the UID (User ID).</td></tr><tr><td><mark style="color:yellow;"><code>pgrep -u &#x3C;username></code></mark></td><td>Retrieves PIDs of processes owned by the user</td></tr><tr><td><mark style="color:yellow;"><code>ps -eo user,pid,cmd</code></mark></td><td>Lists the process owner, process ID, and command for all processes.</td></tr><tr><td><mark style="color:yellow;"><code>top</code></mark></td><td>Provides a dynamic real-time view of system processes, including the user who started each process.</td></tr><tr><td><mark style="color:yellow;"><code>w</code></mark></td><td>Shows all users and their processes.</td></tr><tr><td><mark style="color:yellow;"><code>sacct</code></mark></td><td>If process accounting is enabled, this tool shows historical processes run by users.</td></tr></tbody></table>

## <mark style="color:red;">Jobs</mark>

| `jobs` | Lists active jobs within the current shell. |
| ------ | ------------------------------------------- |

## <mark style="color:red;">Debugging</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="315">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>strace [command]</code></mark></td><td>Traces system calls and signals for a process.</td></tr><tr><td><mark style="color:yellow;"><code>gdb [command]</code></mark></td><td>The GNU Debugger, allows interactive debugging of processes.</td></tr><tr><td><mark style="color:yellow;"><code>strace [command]</code></mark></td><td>Traces system calls and signals for a specific command.</td></tr><tr><td><mark style="color:yellow;"><code>ltrace [command]</code></mark></td><td>Traces library calls for a specific command.</td></tr><tr><td><mark style="color:yellow;"><code>gdb [executable]</code></mark></td><td>The GNU Debugger, used for debugging programs.</td></tr><tr><td><mark style="color:yellow;"><code>valgrind [executable]</code></mark></td><td>A tool for memory debugging, memory leak detection, and profiling.</td></tr><tr><td><mark style="color:yellow;"><code>tcpdump</code></mark></td><td>Captures and displays packets transmitted or received over a network interface.</td></tr><tr><td><mark style="color:yellow;"><code>dmesg</code></mark></td><td>Displays kernel ring buffer messages, useful for diagnosing hardware issues and kernel errors.</td></tr><tr><td><mark style="color:yellow;"><code>tail -f /var/log/syslog</code></mark></td><td>Monitors system log messages in real-time.</td></tr><tr><td><mark style="color:yellow;"><code>strace -p [PID]</code></mark></td><td>Attaches to an existing process and traces its system calls.</td></tr><tr><td><mark style="color:yellow;"><code>lsof</code></mark></td><td>Lists open files and the processes that opened them, helpful for debugging file-related issues.</td></tr><tr><td><mark style="color:yellow;"><code>vmstat</code></mark></td><td>Reports information about processes, memory, paging, block I/O, traps, and CPU activity.</td></tr></tbody></table>

## <mark style="color:red;">Solaris</mark>

| Command                                    | Description                    |
| ------------------------------------------ | ------------------------------ |
| <mark style="color:yellow;">`ptree`</mark> | Show processes in tree format. |
| <mark style="color:yellow;">`ps`</mark>    | Show processes                 |
| <mark style="color:yellow;">`svcs`</mark>  | Dump services                  |
