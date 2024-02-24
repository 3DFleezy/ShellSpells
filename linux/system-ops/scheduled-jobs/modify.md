# Modify

## <mark style="color:red;">Cron Jobs</mark>&#x20;

### <mark style="color:purple;">Modifying Existing Tasks</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>crontab -e</code></td><td>Opens the current user's crontab for editing.</td></tr><tr><td><code>crontab -e -u &#x3C;username></code></td><td>Opens another user's crontab for editing (requires root privileges).</td></tr></tbody></table>

### <mark style="color:purple;">Deleting Tasks</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>crontab -l</code></td><td>Lists all crontab entries.</td></tr><tr><td><code>crontab -r</code></td><td>Removes all entries from the current user's crontab.</td></tr><tr><td><code>crontab -r -u &#x3C;username></code></td><td>Removes all entries from another user's crontab (requires root privileges).</td></tr></tbody></table>

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

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systemctl edit &#x3C;timer_name>.timer</code></td><td>Opens the new timer unit file for editing in your default text editor.</td></tr><tr><td><code>systemd-run --on-active=&#x3C;time> [command]</code></td><td>Creates a transient timer that executes a command after a specified time (e.g., systemd-run --on-active=30 /bin/touch /tmp/foo).</td></tr><tr><td><code>systemd-analyze timers</code></td><td>Analyzes and reports information about existing timers, helping you understand the system's current timer configuration.</td></tr></tbody></table>

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

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systemctl edit &#x3C;timer_name>.timer</code></td><td>Opens the existing timer unit file for editing in your default text editor.</td></tr><tr><td><code>systemctl reload</code></td><td>Reloads systemd after editing the timer unit file to apply changes.</td></tr></tbody></table>

#### <mark style="color:green;">Enabling/Disabling Timers:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systemctl enable &#x3C;timer_name></code></td><td>Enables a timer to start automatically at its scheduled time.</td></tr><tr><td><code>systemctl disable &#x3C;timer_name></code></td><td>Disables a timer from starting automatically.</td></tr></tbody></table>

#### <mark style="color:green;">Manually Start/Stop:</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systemctl start &#x3C;timer_name></code></td><td>Starts a timer manually.</td></tr><tr><td><code>systemctl stop &#x3C;timer_name></code></td><td>Stops a timer manually.</td></tr></tbody></table>

### <mark style="color:purple;">Inspecting Timers</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systemctl list-timers</code></td><td>Lists all active timers along with their next scheduled execution time.</td></tr><tr><td><code>systemctl status mytask.timer</code></td><td>Shows the status of the specified timer, including whether it's active and when it last triggered the service.</td></tr><tr><td><code>systemctl cat mytask.timer</code></td><td>Displays the content of the timer unit file.</td></tr><tr><td><code>systemctl cat mytask.service</code></td><td>Displays the content of the service unit file.</td></tr></tbody></table>



## <mark style="color:red;">Anacron</mark>

### <mark style="color:purple;">Modifying Anacrontab Jobs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>crontab -e</code></td><td>Opens the user's Anacrontab for editing.</td></tr><tr><td><code>ls -l /var/spool/anacron</code></td><td>User anacron jobs are here.</td></tr><tr><td><code>ls -l /etc/anacrontab</code></td><td>ain anacron configuration file</td></tr></tbody></table>

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

<table data-header-hidden data-full-width="true"><thead><tr><th width="350">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>anacron -f</code></td><td>Runs all scheduled tasks immediately, regardless of their scheduled times.</td></tr><tr><td><code>sudo anacron -f -d &#x3C;job_name></code></td><td>Force the execution of a specific Anacron job manually with debug output.</td></tr><tr><td><code>sudo anacron -n</code></td><td>Runs all jobs in the Anacrontab as if anacron had just been started, respecting the delay specified for each job.</td></tr></tbody></table>

## <mark style="color:red;">at</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="352">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>atrm &#x3C;job_id></code></td><td>Removes a specific job from the queue.</td></tr><tr><td><code>atq</code></td><td>View and manipulate tasks scheduled with the <code>at</code> command.</td></tr></tbody></table>

### <mark style="color:purple;">Creating at Jobs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="351">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>at &#x3C;time></code></td><td>Schedules a job to run at a specific time (e.g., at 10:30AM).</td></tr><tr><td><code>at +&#x3C;duration></code></td><td>Schedules a job to run after a specific duration (e.g., at +30 minutes).</td></tr><tr><td><code>at now + 2 hours</code></td><td>Schedules a one-time job to run at a specific time (e.g., 2 hours from now).</td></tr></tbody></table>

Examples: \
`at 10:30AM < /path/to/script.sh`

## <mark style="color:red;">Other Tools</mark>

| Command | Description                                                    |
| ------- | -------------------------------------------------------------- |
| `batch` | Modifies jobs submitted with the batch command (if available). |
