# Modify

## <mark style="color:red;">Systemd (most modern distributions)</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>systemctl start [service_name]</code></td><td>Starts a stopped service.</td></tr><tr><td><code>systemctl stop [service_name]</code></td><td>Stops a running service.</td></tr><tr><td><code>systemctl restart [service_name]</code></td><td>Restarts a running service.</td></tr><tr><td><code>systemctl enable [service_name]</code></td><td>Enables a service to start automatically at boot.</td></tr><tr><td><code>systemctl disable [service_name]</code></td><td>Disables a service from starting automatically at boot.</td></tr><tr><td><code>systemctl reload [service_name]</code></td><td>Reloads the service configuration without restarting it (if supported).</td></tr><tr><td><code>systemctl mask [service_name]</code></td><td>Prevents a service from being started manually or automatically.</td></tr><tr><td><code>systemctl unmask [service_name]</code></td><td>Reverses the effect of mask, allowing the service to be started again.</td></tr></tbody></table>

## <mark style="color:red;">SysV init (older distributions)</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>service [service_name] start</code></td><td>Start</td></tr><tr><td><code>service [service_name] stop</code></td><td>Stop</td></tr><tr><td><code>service [service_name] restart</code></td><td>Restart</td></tr><tr><td><code>service [service_name] reload</code></td><td>Reload</td></tr><tr><td><code>chkconfig [service_name] on</code></td><td>Enables a service at boot.</td></tr><tr><td><code>chkconfig [service_name] off</code></td><td>Disables a service from starting at boot.</td></tr><tr><td><code>update-rc.d [service_name] start &#x3C;runlevels></code></td><td>(SysV init) Enable service in specific runlevels at boot.</td></tr><tr><td><code>chkconfig [service_name] on/off</code></td><td>(SysV init) Enable/disable service for all runlevels.</td></tr></tbody></table>

## <mark style="color:red;">Upstart (rarely used now)</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>start/stop/restart [service_name]</code></td><td>Service commands.</td></tr><tr><td><code>initctl start [service_name]</code></td><td>Starts a service.</td></tr><tr><td><code>initctl stop [service_name]</code></td><td>Stops a service.</td></tr></tbody></table>
