# Modify

| Command                       | Description                                                                                |
| ----------------------------- | ------------------------------------------------------------------------------------------ |
| `kill [PID]`                  | Sends a termination signal to a process (SIGTERM by default).                              |
| `kill -9 [PID]`               | Sends a forceful termination signal (SIGKILL).                                             |
| `kill -15 [PID]`              | Sends the graceful termination signal (SIGTERM) to a process.                              |
| `killall [process_name]`      | Terminates all processes with a matching name.                                             |
| `pkill [process_name]`        | Terminates processes based on their name.                                                  |
| `bg [job_number]`             | Moves a suspended job to the background.                                                   |
| `fg [job_number]`             | Brings a background job to the foreground.                                                 |
| `ctrl+z`                      | Suspends the current foreground process in the terminal.                                   |
| `nice <priority> [command]`   | Runs a command with a lower priority.                                                      |
| `renice [PID] [new_priority]` | Changes priority of a running process.                                                     |
| `nohup command &`             | Runs a command immune to hangups, with output to a non-tty.                                |
| `disown %jobnumber`           | Removes a job from the shell's job table, making it immune to signals from the shell.      |
| `disown [PID]`                | Removes a process from the shell's job table, preventing it from receiving SIGHUP signals. |
