# Enumerate

## <mark style="color:red;">Cron Jobs</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>find /etc/cron* -print</code></td><td>Shows all crontab files across the system (requires root privileges).</td></tr><tr><td><code>crontab -l</code></td><td>Lists the current user's crontab entries.</td></tr><tr><td><code>crontab -u &#x3C;username> -l</code></td><td>Lists crontab entries for a specific user (requires superuser privileges).</td></tr><tr><td><code>cat /etc/crontab</code></td><td>Displays the system's main crontab, which might contain system-wide scheduled tasks.</td></tr><tr><td><code>ls -l /etc/cron*</code></td><td>Lists system-wide crontabs directories and files (requires root privileges).</td></tr><tr><td><code>ls /etc/cron.d/</code></td><td>Lists cron job files in the <code>/etc/cron.d/</code> directory for individual cron jobs.</td></tr><tr><td><code>ls /etc/cron.hourly/</code></td><td>Lists scripts scheduled to run every hour.</td></tr><tr><td><code>ls /etc/cron.daily/</code></td><td>Lists scripts scheduled to run daily.</td></tr><tr><td><code>ls /etc/cron.weekly/</code></td><td>Lists scripts scheduled to run weekly.</td></tr><tr><td><code>ls /etc/cron.monthly/</code></td><td>Lists scripts scheduled to run monthly.</td></tr><tr><td><code>cat /etc/anacrontab</code></td><td>Displays tasks scheduled with anacron for systems that don't run 24/7.</td></tr><tr><td><code>systemctl list-timers</code></td><td>Lists active systemd timers, showing schedules and last trigger times.</td></tr><tr><td><code>ls /var/spool/cron/crontabs/</code></td><td>Lists the directories for user-specific cron jobs, typically requires superuser access.</td></tr></tbody></table>

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

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>find /etc/systemd/system -name "*.timer"</code></td><td>Lists all timer unit files (requires root privileges).</td></tr><tr><td><code>systemctl list-timers</code></td><td>Lists all active timers along with their next scheduled execution time and the last time they were triggered.</td></tr><tr><td><code>systemctl list-timers --all</code></td><td>Lists all timers, including inactive ones, showing their next scheduled execution time and the last time they were triggered.</td></tr><tr><td><code>systemctl list-timers --state=active</code></td><td>Lists only active timers that are currently scheduled to run.</td></tr><tr><td><code>systemctl list-timers --state=inactive</code></td><td>Lists only inactive timers that have not yet been triggered.</td></tr><tr><td><code>systemctl list-timers --state=disabled</code></td><td>Lists only disabled timers that are not scheduled to run at all.</td></tr><tr><td><code>systemctl list-timers grep &#x3C;keyword></code></td><td>Filter the output based on keywords in the timer unit names or descriptions.</td></tr><tr><td><code>systemctl status &#x3C;timer_name></code></td><td>Shows detailed information about a specific timer.</td></tr><tr><td><code>systemctl cat &#x3C;timer_name></code></td><td>Displays the full unit file configuration for a specific timer, showing how it's configured to run.</td></tr><tr><td><code>systemctl list-unit-files --type=timer</code></td><td>Lists all installed timer unit files, showing their enabled/disabled state.</td></tr><tr><td><code>journalctl -u &#x3C;timer_name></code></td><td>Shows the journal logs for a specific timer, useful for troubleshooting or checking what the timer did when it last ran.</td></tr><tr><td><code>systemctl show &#x3C;timer_name></code></td><td>Shows low-level details about a specific timer unit in a property=value format.</td></tr></tbody></table>



## <mark style="color:red;">Anacron</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>anacron -t</code></td><td>Displays tasks scheduled by anacron and their next run times.</td></tr><tr><td><code>anacron -l</code></td><td>Shows logs of previous anacron runs.</td></tr><tr><td><code>find /etc/anacrontab -print</code></td><td>Locates the main anacron configuration file (requires root privileges).</td></tr><tr><td><code>crontab -l</code></td><td>(Not an Anacron command, but commonly used) List the tasks in the current user's Anacrontab.</td></tr><tr><td><code>cat /etc/anacrontab</code></td><td>Anacrontab location.</td></tr></tbody></table>

### <mark style="color:purple;">Spool Directory</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="383">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>ls -l /var/spool/anacron&#x3C;username></code></td><td>This directory contains individual files for each user's Anacron jobs. The file names correspond to the time intervals used by Anacron (e.g.,hourly,daily,weekly,monthly)</td></tr><tr><td><code>ls -l /var/spool/anacron/root</code></td><td>Contains Anacron jobs for the root user</td></tr></tbody></table>

### <mark style="color:purple;">Analyze Timestamps</mark>

`ls -l /var/log/anacron`\
Anacron logs its activity here.&#x20;

Look for lines starting with "running job file" followed by the filename and username.&#x20;

The timestamp indicates the last execution time.



## <mark style="color:red;">at</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>atq</code></td><td>Lists jobs scheduled using the <code>at</code> command.</td></tr><tr><td><code>atq -la</code></td><td>Similar to <code>atq</code>, but might provide more detailed information like priority and working directory.</td></tr><tr><td><code>atq -v</code></td><td>Provides more detailed information about each job, including its ID, time, command, and user.</td></tr><tr><td><code>atq -u &#x3C;user></code></td><td>Filters jobs for a specific user.</td></tr><tr><td><code>at -c &#x3C;job number></code></td><td>Shows the command for a specific job.</td></tr><tr><td><code>ls -l /var/spool/cron/atjobs</code></td><td>Lists the at jobs directory to view job files, requires superuser access.</td></tr><tr><td><code>ls -l /var/spool/at</code></td><td>Another common location for at job files on some Unix systems, requires superuser access.</td></tr><tr><td><code>ls -l /var/spool/cron/&#x3C;username></code></td><td>User jobs stored here.</td></tr><tr><td><code>/etc/at.allow or /etc/at.deny</code></td><td>Controls who can use the <code>at</code> command for scheduling jobs.</td></tr></tbody></table>

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
