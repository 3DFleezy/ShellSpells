# Enumerate

## <mark style="color:red;">Cron Jobs</mark>

| Command                        | Description                                                                             |
| ------------------------------ | --------------------------------------------------------------------------------------- |
| `find /etc/cron* -print`       | Shows all crontab files across the system (requires root privileges).                   |
| `crontab -l`                   | Lists the current user's crontab entries.                                               |
| `crontab -u <username> -l`     | Lists crontab entries for a specific user (requires superuser privileges).              |
| `cat /etc/crontab`             | Displays the system's main crontab, which might contain system-wide scheduled tasks.    |
| `ls -l /etc/cron*`             | Lists system-wide crontabs directories and files (requires root privileges).            |
| `ls /etc/cron.d/`              | Lists cron job files in the `/etc/cron.d/` directory for individual cron jobs.          |
| `ls /etc/cron.hourly/`         | Lists scripts scheduled to run every hour.                                              |
| `ls /etc/cron.daily/`          | Lists scripts scheduled to run daily.                                                   |
| `ls /etc/cron.weekly/`         | Lists scripts scheduled to run weekly.                                                  |
| `ls /etc/cron.monthly/`        | Lists scripts scheduled to run monthly.                                                 |
| `cat /etc/anacrontab`          | Displays tasks scheduled with anacron for systems that don't run 24/7.                  |
| `systemctl list-timers`        | Lists active systemd timers, showing schedules and last trigger times.                  |
| `ls /var/spool/cron/crontabs/` | Lists the directories for user-specific cron jobs, typically requires superuser access. |

Show crontabs for each user:

{% code overflow="wrap" %}
```bash
for user in $(cut -f1 -d: /etc/passwd); do echo $user >> /tmp/crontabs; crontab -u $user -l >> /tmp/crontabs; done
```
{% endcode %}

Prints the contents of all system-wide cron job files:

```bash
find /etc/cron.* -type f -exec cat {} +
```

Prints the contents of all user-specific cron jobs, requires superuser access:

```bash
find /var/spool/cron/crontabs -type f -exec cat {} +
```

Lists all current users and their cron jobs (requires root privileges):

```bash
who | awk '{print $1}' | xargs -n1 crontab -u -l
```



## <mark style="color:red;">Systemd Timers</mark>

| Command                                    | Description                                                                                                                   |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| `find /etc/systemd/system -name "*.timer"` | Lists all timer unit files (requires root privileges).                                                                        |
| `systemctl list-timers`                    | Lists all active timers along with their next scheduled execution time and the last time they were triggered.                 |
| `systemctl list-timers --all`              | Lists all timers, including inactive ones, showing their next scheduled execution time and the last time they were triggered. |
| `systemctl list-timers --state=active`     | Lists only active timers that are currently scheduled to run.                                                                 |
| `systemctl list-timers --state=inactive`   | Lists only inactive timers that have not yet been triggered.                                                                  |
| `systemctl list-timers --state=disabled`   | Lists only disabled timers that are not scheduled to run at all.                                                              |
| `systemctl list-timers grep <keyword>`     | Filter the output based on keywords in the timer unit names or descriptions.                                                  |
| `systemctl status <timer_name>`            | Shows detailed information about a specific timer.                                                                            |
| `systemctl cat <timer_name>`               | Displays the full unit file configuration for a specific timer, showing how it's configured to run.                           |
| `systemctl list-unit-files --type=timer`   | Lists all installed timer unit files, showing their enabled/disabled state.                                                   |
| `journalctl -u <timer_name>`               | Shows the journal logs for a specific timer, useful for troubleshooting or checking what the timer did when it last ran.      |
| `systemctl show <timer_name>`              | Shows low-level details about a specific timer unit in a property=value format.                                               |



## <mark style="color:red;">Anacron</mark>

| Command                       | Description                                                                                  |
| ----------------------------- | -------------------------------------------------------------------------------------------- |
| `anacron -t`                  | Displays tasks scheduled by anacron and their next run times.                                |
| `anacron -l`                  | Shows logs of previous anacron runs.                                                         |
| `find /etc/anacrontab -print` | Locates the main anacron configuration file (requires root privileges).                      |
| `crontab -l`                  | (Not an Anacron command, but commonly used) List the tasks in the current user's Anacrontab. |
| `cat /etc/anacrontab`         | Anacrontab location.                                                                         |

### <mark style="color:purple;">Spool Directory</mark>

<table><thead><tr><th width="383">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>ls -l /var/spool/anacron&#x3C;username></code></td><td>This directory contains individual files for each user's Anacron jobs. The file names correspond to the time intervals used by Anacron (e.g.,hourly,daily,weekly,monthly)</td></tr><tr><td><code>ls -l /var/spool/anacron/root</code></td><td>Contains Anacron jobs for the root user</td></tr></tbody></table>

### <mark style="color:purple;">Analyze Timestamps</mark>

`ls -l /var/log/anacron`\
Anacron logs its activity here.&#x20;

Look for lines starting with "running job file" followed by the filename and username.&#x20;

The timestamp indicates the last execution time.



## <mark style="color:red;">at</mark>

| Command                            | Description                                                                                        |
| ---------------------------------- | -------------------------------------------------------------------------------------------------- |
| `atq`                              | Lists jobs scheduled using the `at` command.                                                       |
| `atq -la`                          | Similar to `atq`, but might provide more detailed information like priority and working directory. |
| `atq -v`                           | Provides more detailed information about each job, including its ID, time, command, and user.      |
| `atq -u <user>`                    | Filters jobs for a specific user.                                                                  |
| `at -c <job number>`               | Shows the command for a specific job.                                                              |
| `ls -l /var/spool/cron/atjobs`     | Lists the at jobs directory to view job files, requires superuser access.                          |
| `ls -l /var/spool/at`              | Another common location for at job files on some Unix systems, requires superuser access.          |
| `ls -l /var/spool/cron/<username>` | User jobs stored here.                                                                             |
| `/etc/at.allow or /etc/at.deny`    | Controls who can use the `at` command for scheduling jobs.                                         |

Lists job numbers along with their owners by extracting user information from job details:

```bash
sudo atq | awk '{print $1}' | xargs -I {} sudo at -c {} | grep '^<'
```

Loops through all pending jobs for the current user, displaying details of each:

```bash
for job in $(atq | awk '{print $1}'); do at -c $job; done
```



## <mark style="color:red;">Other Tools</mark>

| Command    | Description                                                      |
| ---------- | ---------------------------------------------------------------- |
| `batch -l` | Displays jobs submitted with the `batch` command (if available). |
