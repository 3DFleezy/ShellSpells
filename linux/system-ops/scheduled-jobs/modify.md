# Modify

## <mark style="color:red;">Cron Jobs</mark>&#x20;

### <mark style="color:purple;">Modifying Existing Tasks</mark>

| Command                    | Description                                                          |
| -------------------------- | -------------------------------------------------------------------- |
| `crontab -e`               | Opens the current user's crontab for editing.                        |
| `crontab -e -u <username>` | Opens another user's crontab for editing (requires root privileges). |

### <mark style="color:purple;">Deleting Tasks</mark>

| Command                    | Description                                                                 |
| -------------------------- | --------------------------------------------------------------------------- |
| `crontab -l`               | Lists all crontab entries.                                                  |
| `crontab -r`               | Removes all entries from the current user's crontab.                        |
| `crontab -r -u <username>` | Removes all entries from another user's crontab (requires root privileges). |

Edit the crontab file to comment out or remove specific lines.

Examples: \
Run a script every hour: `0 * * * * /path/to/script.sh` \
Backup files daily at midnight: `0 0 * * * tar -czf /path/to/backup.tar.gz /path/to/files` \
Send an email weekly on Sundays: `0 0 * * 0 mail -s "Weekly Report" user@example.com < /path/to/report.txt` \
Run a backup script at 3 am every day: `0 3 * * * /path/to/backup_script.sh`



```
* * * * * command to execute
- - - - -
| | | | |
| | | | +------------ Day of the week (0 - 7) (Sunday=0 or 7)
| | | +------------ Month (1 - 12)
| | +------------ Day of the month (1 - 31)
| +------------ Hour (0 - 23)
+------------ Minute (0 - 59)
```



## <mark style="color:red;">Systemd Timers</mark>

### <mark style="color:purple;">Example Workflow</mark>

Create the <mark style="color:orange;">**service**</mark> unit that specifies what command or script to run. \
Create the <mark style="color:orange;">**timer**</mark> unit that specifies when the service should be triggered. \
Start and <mark style="color:orange;">**enable**</mark> the timer to ensure it runs as scheduled. \
<mark style="color:orange;">**Inspect**</mark> the timer as needed to verify its configuration and status. <==

### <mark style="color:purple;">Creating a Service Unit</mark>

Create a .service file in /etc/systemd/system/ for your task. \
For example, mytask.service:

```
[Unit]
Description=Example systemd service.

[Service]
Type=simple
ExecStart=/path/to/your/script.sh
```

### <mark style="color:purple;">Creating New Timer Unit</mark>

| Command                                    | Description                                                                                                                      |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| `systemctl edit <timer_name>.timer`        | Opens the new timer unit file for editing in your default text editor.                                                           |
| `systemd-run --on-active=<time> [command]` | Creates a transient timer that executes a command after a specified time (e.g., systemd-run --on-active=30 /bin/touch /tmp/foo). |
| `systemd-analyze timers`                   | Analyzes and reports information about existing timers, helping you understand the system's current timer configuration.         |

Create a corresponding .timer file in the same directory. For example, mytask.timer:

```
[Unit]
Description=Timer for mytask

[Timer]
OnBootSec=15min
OnUnitActiveSec=24h
Unit=mytask.service

[Install]
WantedBy=timers.target
```

### <mark style="color:purple;">Managing Systemd Timers</mark>

#### <mark style="color:green;">Editing an existing timer</mark>:

| Command                             | Description                                                                 |
| ----------------------------------- | --------------------------------------------------------------------------- |
| `systemctl edit <timer_name>.timer` | Opens the existing timer unit file for editing in your default text editor. |
| `systemctl reload`                  | Reloads systemd after editing the timer unit file to apply changes.         |

#### <mark style="color:green;">Enabling/Disabling Timers:</mark>

| Command                          | Description                                                   |
| -------------------------------- | ------------------------------------------------------------- |
| `systemctl enable <timer_name>`  | Enables a timer to start automatically at its scheduled time. |
| `systemctl disable <timer_name>` | Disables a timer from starting automatically.                 |

#### <mark style="color:green;">Manually Start/Stop:</mark>

| Command                        | Description              |
| ------------------------------ | ------------------------ |
| `systemctl start <timer_name>` | Starts a timer manually. |
| `systemctl stop <timer_name>`  | Stops a timer manually.  |

### <mark style="color:purple;">Inspecting Timers</mark>

| Command                         | Description                                                                                                    |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `systemctl list-timers`         | Lists all active timers along with their next scheduled execution time.                                        |
| `systemctl status mytask.timer` | Shows the status of the specified timer, including whether it's active and when it last triggered the service. |
| `systemctl cat mytask.timer`    | Displays the content of the timer unit file.                                                                   |
| `systemctl cat mytask.service`  | Displays the content of the service unit file.                                                                 |



## <mark style="color:red;">Anacron</mark>

### <mark style="color:purple;">Modifying Anacrontab Jobs</mark>

| Command                    | Description                              |
| -------------------------- | ---------------------------------------- |
| `crontab -e`               | Opens the user's Anacrontab for editing. |
| `ls -l /var/spool/anacron` | User anacron jobs are here.              |
| `ls -l /etc/anacrontab`    | ain anacron configuration file           |

Edit the entries like a standard crontab, but use specific Anacron time specifiers (e.g., "daily", "10d").

Example: \
`sudo vim /etc/anacrontab`\
add the following to create a new anacron job that runs a script daily, even if the system is not always on:\
`1 5 my_daily_script /path/to/script.sh`\
`[period] [delay] [job-identifier] [command]`

| `period`         | How often the job should run, in days.                         |
| ---------------- | -------------------------------------------------------------- |
| `delay`          | Delay in minutes before starting the job after anacron starts. |
| `job-identifier` | A unique name for the job's log file.                          |
| `command`        | The command or script to be executed.                          |

### <mark style="color:purple;">Creating Anacron Jobs</mark>

Example: \
Run a script every 3 hours with a random delay of 60 minutes:\
`360 * /path/to/script.sh`

### <mark style="color:purple;">Forcing Task Execution:</mark>

| Command                         | Description                                                                                                       |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `anacron -f`                    | Runs all scheduled tasks immediately, regardless of their scheduled times.                                        |
| `sudo anacron -f -d <job_name>` | Force the execution of a specific Anacron job manually with debug output.                                         |
| `sudo anacron -n`               | Runs all jobs in the Anacrontab as if anacron had just been started, respecting the delay specified for each job. |

## <mark style="color:red;">at</mark>

| Command         | Description                                                |
| --------------- | ---------------------------------------------------------- |
| `atrm <job_id>` | Removes a specific job from the queue.                     |
| `atq`           | View and manipulate tasks scheduled with the `at` command. |

### <mark style="color:purple;">Creating at Jobs</mark>

| Command            | Description                                                                  |
| ------------------ | ---------------------------------------------------------------------------- |
| `at <time>`        | Schedules a job to run at a specific time (e.g., at 10:30AM).                |
| `at +<duration>`   | Schedules a job to run after a specific duration (e.g., at +30 minutes).     |
| `at now + 2 hours` | Schedules a one-time job to run at a specific time (e.g., 2 hours from now). |

Examples: \
`at 10:30AM < /path/to/script.sh`

## <mark style="color:red;">Other Tools</mark>

| Command | Description                                                    |
| ------- | -------------------------------------------------------------- |
| `batch` | Modifies jobs submitted with the batch command (if available). |
