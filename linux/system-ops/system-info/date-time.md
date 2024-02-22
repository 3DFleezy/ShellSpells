# Date/Time

## Enumerate

### Date/Time Info

| Command                        | Description                                                   |
| ------------------------------ | ------------------------------------------------------------- |
| `date`                         | Display the current date and time                             |
| `date +"%Y-%m-%d %H:%M:%S %Z"` | Custom format: YYYY-MM-DD HH:MM:SS TZ                         |
| `hwclock`                      | Displays hardware clock time (if different from system time). |
| `hwclock --show`               | Displays the hardware clock time.                             |
| `timedatectl`                  | Displays current timezone and other time-related settings.    |
| `ntpq -p`                      | Displays current NTP synchronization status.                  |
| `uptime`                       | Shows system uptime and load averages.                        |
| `date +%s`                     | Current Epoch Time (Seconds from January 1, 1970).            |
| `cal`                          | Displays a calendar for the current month.                    |
