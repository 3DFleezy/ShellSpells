# Enumerate

## <mark style="color:red;">All Systems</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="454">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>cat /etc/services</code></td><td>Display network services</td></tr><tr><td><code>service --status-all</code></td><td>Shows all services</td></tr><tr><td><code>ps aux | grep [service_name]</code></td><td>Lists processes related to a specific service.</td></tr><tr><td><code>netstat -tlpn | grep [service_name]</code></td><td>Shows network connections used by a service.</td></tr><tr><td><code>ss -tulnp</code></td><td>Another command to display active network connections and associated services</td></tr></tbody></table>

## <mark style="color:red;">Systemd (most modern distributions):</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="454">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systemctl</code></td><td>Lists units for systemd, implicitly including services.</td></tr><tr><td><code>systemctl list-unit-files</code></td><td>Lists all available systemd unit files, including services.</td></tr><tr><td><code>systemctl list-units</code></td><td>Shows currently running services and their status.</td></tr><tr><td><code>systemctl list-units --type=service --all</code></td><td>Lists all systemd services, including active and inactive.</td></tr><tr><td><code>systemctl status [service_name]</code></td><td>Displays detailed information about a specific service.</td></tr><tr><td><code>systemctl enable/disable [service_name]</code></td><td>Enables or disables a service for automatic startup.</td></tr></tbody></table>

## <mark style="color:red;">SysV init (older distributions):</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="458">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>/etc/init.d</code></td><td>Directory containing service scripts.</td></tr><tr><td><code>ls /etc/init.d</code></td><td>Lists all service scripts in the directory.</td></tr><tr><td><code>service --status-all</code></td><td>Displays the status of all services.</td></tr><tr><td><code>service [service_name] status</code></td><td>Checks the status of a specific service.</td></tr><tr><td><code>service [service_name] start/stop/restart</code></td><td>Starts, stops, or restarts a service.</td></tr><tr><td><code>chkconfig --list</code></td><td>Lists all services and their runlevel settings.</td></tr></tbody></table>

## <mark style="color:red;">Upstart (rarely used now):</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="459">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>status [service_name]</code></td><td>Shows the status of a specific service.</td></tr><tr><td><code>stop [service_name]</code></td><td>Stops a service.</td></tr><tr><td><code>start [service_name]</code></td><td>Starts a service.</td></tr><tr><td><code>initctl list</code></td><td>Lists all running Upstart jobs.</td></tr></tbody></table>
