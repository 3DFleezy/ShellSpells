# Enumerate

## <mark style="color:red;">All Systems</mark>

| Command                | Description                                                                   |
| ---------------------- | ----------------------------------------------------------------------------- |
| `cat /etc/services`    | Display network services                                                      |
| `service --status-all` | Shows all services                                                            |
| \`ps aux               | grep \[service\_name]\`                                                       |
| \`netstat -tlpn        | grep \[service\_name]\`                                                       |
| `ss -tulnp`            | Another command to display active network connections and associated services |

## <mark style="color:red;">Systemd (most modern distributions):</mark>

| Command                                     | Description                                                 |
| ------------------------------------------- | ----------------------------------------------------------- |
| `systemctl`                                 | Lists units for systemd, implicitly including services.     |
| `systemctl list-unit-files`                 | Lists all available systemd unit files, including services. |
| `systemctl list-units`                      | Shows currently running services and their status.          |
| `systemctl list-units --type=service --all` | Lists all systemd services, including active and inactive.  |
| `systemctl status [service_name]`           | Displays detailed information about a specific service.     |
| `systemctl enable/disable [service_name]`   | Enables or disables a service for automatic startup.        |

## <mark style="color:red;">SysV init (older distributions):</mark>

| Command                                     | Description                                     |
| ------------------------------------------- | ----------------------------------------------- |
| `/etc/init.d`                               | Directory containing service scripts.           |
| `ls /etc/init.d`                            | Lists all service scripts in the directory.     |
| `service --status-all`                      | Displays the status of all services.            |
| `service [service_name] status`             | Checks the status of a specific service.        |
| `service [service_name] start/stop/restart` | Starts, stops, or restarts a service.           |
| `chkconfig --list`                          | Lists all services and their runlevel settings. |

## <mark style="color:red;">Upstart (rarely used now):</mark>

| Command                 | Description                             |
| ----------------------- | --------------------------------------- |
| `status [service_name]` | Shows the status of a specific service. |
| `stop [service_name]`   | Stops a service.                        |
| `start [service_name]`  | Starts a service.                       |
| `initctl list`          | Lists all running Upstart jobs.         |
