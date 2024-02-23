---
description: System time and timezone information.
---

# Date/Time

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Date/Time Info</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="348">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>date</code></mark></td><td>Display the current date and time</td></tr><tr><td><mark style="color:yellow;"><code>date +"%Y-%m-%d %H:%M:%S %Z"</code></mark></td><td>Custom format: YYYY-MM-DD HH:MM:SS TZ</td></tr><tr><td><mark style="color:yellow;"><code>hwclock</code></mark></td><td>Displays hardware clock time (if different from system time).</td></tr><tr><td><mark style="color:yellow;"><code>hwclock --show</code></mark></td><td>Displays the hardware clock time.</td></tr><tr><td><mark style="color:yellow;"><code>timedatectl</code></mark></td><td>Displays current timezone and other time-related settings.</td></tr><tr><td><mark style="color:yellow;"><code>ntpq -p</code></mark></td><td>Displays current NTP synchronization status.</td></tr><tr><td><mark style="color:yellow;"><code>uptime</code></mark></td><td>Shows system uptime and load averages.</td></tr><tr><td><mark style="color:yellow;"><code>date +%s</code></mark></td><td>Current Epoch Time (Seconds from January 1, 1970).</td></tr><tr><td><mark style="color:yellow;"><code>cal</code></mark></td><td>Displays a calendar for the current month.</td></tr></tbody></table>

### <mark style="color:purple;">Timezone Info</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="350">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>cat /etc/timezone</code></mark></td><td>Displays the system's timezone (Debian-based systems).</td></tr><tr><td><mark style="color:yellow;"><code>ls /usr/share/zoneinfo</code></mark></td><td>Lists available timezones.</td></tr><tr><td><mark style="color:yellow;"><code>timedatectl list-timezones</code></mark></td><td>Lists all timezones (systemd systems).</td></tr><tr><td><mark style="color:yellow;"><code>date +%Z</code></mark></td><td>Shows the timezone abbreviation.</td></tr><tr><td><mark style="color:yellow;"><code>zdump /etc/localtime</code></mark></td><td>Shows the timezone based on the /etc/localtime file.</td></tr><tr><td><mark style="color:yellow;"><code>TZ='America/New_York' date</code></mark></td><td>Displays date/time info for specified timezone without changing system settings.</td></tr></tbody></table>

## <mark style="color:red;">Modify</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="464">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>date --set="2024-02-04 15:30:00"</code></mark></td><td>Sets system time and date.</td></tr><tr><td><mark style="color:yellow;"><code>sudo date --set="2024-02-04 15:30:00"</code></mark></td><td>Sets system time and date with admin privileges.</td></tr><tr><td><mark style="color:yellow;"><code>hwclock --set --date="2024-02-04 15:30:00"</code></mark></td><td>Sets hardware clock time (requires root access).</td></tr><tr><td><mark style="color:yellow;"><code>timedatectl set-timezone &#x3C;timezone></code></mark></td><td>Sets timezone (e.g., "America/Los_Angeles").</td></tr><tr><td><mark style="color:yellow;"><code>sudo hwclock --systohc</code></mark></td><td>Writes system time to hardware clock.</td></tr><tr><td><mark style="color:yellow;"><code>sudo hwclock --hctosys</code></mark></td><td>Reads hardware clock time and sets system time.</td></tr><tr><td><mark style="color:yellow;"><code>ntpdate pool.ntp.org</code></mark></td><td>Synchronizes time with a public NTP server.</td></tr><tr><td><mark style="color:yellow;"><code>systemctl start ntpd</code></mark></td><td>Starts the NTP daemon for automatic synchronization.</td></tr></tbody></table>

## <mark style="color:red;">Time-based Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>timeout &#x3C;seconds> &#x3C;command></code></mark></td><td>Runs a command with a time limit.</td></tr><tr><td><mark style="color:yellow;"><code>watch -n &#x3C;seconds> &#x3C;command></code></mark></td><td>Repeatedly executes a command, showing output.</td></tr></tbody></table>

## <mark style="color:red;">File Locations</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="247">Path</th><th>Description</th></tr></thead><tbody><tr><td>/usr/share/zoneinfo</td><td>Timezone information directory.</td></tr><tr><td>/etc/timezone</td><td>Stores the system's default timezone (Debian-based systems).</td></tr><tr><td>/etc/localtime</td><td>A symlink or copy of the timezone information file from /usr/share/zoneinfo.</td></tr><tr><td>/etc/sysconfig/clock</td><td>Stores timezone settings on some Linux distributions (e.g., Red Hat-based systems).</td></tr><tr><td>/etc/sysconfig/timezone</td><td>Stores timezone settings on some Linux distributions (e.g., Red Hat-based systems).</td></tr></tbody></table>
