# Enumerate

## <mark style="color:red;">Process Observation</mark>

| Command                  | Description                                                   |
| ------------------------ | ------------------------------------------------------------- |
| `systemd-cgls`           | Shows process additional context. Useful for finding malware. |
| `ps -A`                  | View all running processes                                    |
| `ps axjf`                | Process tree                                                  |
| `pstree`                 | Process tree                                                  |
| `ps -auxf`               | Processes including CPU and MEM                               |
| `ps -efH`                | Processes using standard syntax with process hierarchy        |
| `/proc/version`          | Info about system processes                                   |
| `lsof`                   | Lists all open files belonging to all active processes        |
| `lsof -c <command_name>` | Listing of files for processes executing the command          |
| \`lsof -i <4             | 6>\`                                                          |
| `top`                    | Display real-time system statistics                           |
| `top -u <username>`      | User-specific processes                                       |
| `htop`                   | Interactive process viewer (May need install)                 |

### <mark style="color:purple;">Identifying Suspicious Activity</mark>

Network connections: View open network connections and identify processes making unusual connections. Resource usage: Processes consuming excessive resources might be suspicious. File access: Monitor file access to identify processes accessing sensitive files or system locations.



## <mark style="color:red;">PID</mark>

### <mark style="color:purple;">Finding Process PIDs</mark>

| Command                | Description                                 |
| ---------------------- | ------------------------------------------- |
| `pidof [process_name]` | Finds the PIDs of running processes by name |
| `pgrep [process_name]` | Finds process IDs for matching processes    |

### <mark style="color:purple;">Finding Processes by PIDs</mark>

| Command                             | Description                                                                            |
| ----------------------------------- | -------------------------------------------------------------------------------------- |
| `ps -p [PID]`                       | Displays information for a specific process ID.                                        |
| `ps -fp [PID]`                      | Info about a specific process, given its process ID (PID)                              |
| `pgrep [pattern]`                   | Lists process IDs matching a pattern.                                                  |
| `lsof -p [PID]`                     | Lists all open files by PID.                                                           |
| `ls -al /proc/[PID]`                | Shows the PIDs of processes in `/proc`.                                                |
| `cat /proc/[PID]/maps`              | Displays the memory mappings of a specific process identified by its process ID (PID). |
| `ls -al /proc/[PID]/fd \| grep \\/` | Shows only directories                                                                 |
| `readlink -f /proc/[PID]/exe`       | Examines running processes                                                             |

## <mark style="color:red;">Process Name</mark>

| Command                          | Description                                                                          |
| -------------------------------- | ------------------------------------------------------------------------------------ |
| `grep [process_name] /var/log/*` | Search through all files in the directory for a file containing \[process\_name].    |
| `tail -f /var/log/messages`      | Prints the last 10 lines of `/var/log/messages` and monitors the file for new lines. |
| `find / -name *[process_name]*`  | Starting in "/", find something containing the phrase \[process\_name]               |
| \`chkconfig --list               | grep \[process\_name]\`                                                              |
| `chkconfig --list`               | Queries runlevel info for system services.                                           |
| `ps -p [PID] -o comm=`           | Displays the name of the process with the specified PID.                             |



## <mark style="color:red;">Shared Objects</mark>

| Command                                                | Description                                                                            |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| \`lsof -N -n                                           | grep '.so'\`                                                                           |
| `find /proc/*/maps -type f -exec grep -H '\.so' {} \;` | Inspects processes and their mapped shared objects directly using the proc filesystem. |
| \`pmap \[PID]                                          | grep '/lib/'\`                                                                         |
| \`ldd /executable                                      | grep '/lib/'\`                                                                         |

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

| Command               | Description                                                                                         |
| --------------------- | --------------------------------------------------------------------------------------------------- |
| `ps aux`              | Processes for all users                                                                             |
| `ps -u <username>`    | Lists processes running under a specific user.                                                      |
| \`ps aux              | grep euid=<-UUID>\`                                                                                 |
| \`ps aux              | grep root\`                                                                                         |
| `ps -U UID`           | Shows processes for a user specified by the UID (User ID).                                          |
| `pgrep -u <username>` | Retrieves PIDs of processes owned by the user                                                       |
| `ps -eo user,pid,cmd` | Lists the process owner, process ID, and command for all processes.                                 |
| `top`                 | Provides a dynamic real-time view of system processes, including the user who started each process. |
| `w`                   | Shows all users and their processes.                                                                |
| `sacct`               | If process accounting is enabled, this tool shows historical processes run by users.                |

## <mark style="color:red;">Jobs</mark>

| Command | Description                                 |
| ------- | ------------------------------------------- |
| `jobs`  | Lists active jobs within the current shell. |



## <mark style="color:red;">Debugging</mark>

| Command                   | Description                                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------------------- |
| `strace [command]`        | Traces system calls and signals for a process.                                                  |
| `gdb [command]`           | The GNU Debugger, allows interactive debugging of processes.                                    |
| `strace [command]`        | Traces system calls and signals for a specific command.                                         |
| `ltrace [command]`        | Traces library calls for a specific command.                                                    |
| `gdb [executable]`        | The GNU Debugger, used for debugging programs.                                                  |
| `valgrind [executable]`   | A tool for memory debugging, memory leak detection, and profiling.                              |
| `tcpdump`                 | Captures and displays packets transmitted or received over a network interface.                 |
| `dmesg`                   | Displays kernel ring buffer messages, useful for diagnosing hardware issues and kernel errors.  |
| `tail -f /var/log/syslog` | Monitors system log messages in real-time.                                                      |
| `strace -p [PID]`         | Attaches to an existing process and traces its system calls.                                    |
| `lsof`                    | Lists open files and the processes that opened them, helpful for debugging file-related issues. |
| `vmstat`                  | Reports information about processes, memory, paging, block I/O, traps, and CPU activity.        |



## <mark style="color:red;">Solaris</mark>

| Command | Description                    |
| ------- | ------------------------------ |
| `ptree` | Show processes in tree format. |
| `ps`    | Show processes                 |
| `svcs`  | Dump services                  |
