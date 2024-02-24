# Modify

## <mark style="color:red;">Systemd (most modern distributions)</mark>

| Command                            | Description                                                             |
| ---------------------------------- | ----------------------------------------------------------------------- |
| `systemctl start [service_name]`   | Starts a stopped service.                                               |
| `systemctl stop [service_name]`    | Stops a running service.                                                |
| `systemctl restart [service_name]` | Restarts a running service.                                             |
| `systemctl enable [service_name]`  | Enables a service to start automatically at boot.                       |
| `systemctl disable [service_name]` | Disables a service from starting automatically at boot.                 |
| `systemctl reload [service_name]`  | Reloads the service configuration without restarting it (if supported). |
| `systemctl mask [service_name]`    | Prevents a service from being started manually or automatically.        |
| `systemctl unmask [service_name]`  | Reverses the effect of mask, allowing the service to be started again.  |

## <mark style="color:red;">SysV init (older distributions)</mark>

| Command                                        | Description                                               |
| ---------------------------------------------- | --------------------------------------------------------- |
| `service [service_name] start`                 | Start                                                     |
| `service [service_name] stop`                  | Stop                                                      |
| `service [service_name] restart`               | Restart                                                   |
| `service [service_name] reload`                | Reload                                                    |
| `chkconfig [service_name] on`                  | Enables a service at boot.                                |
| `chkconfig [service_name] off`                 | Disables a service from starting at boot.                 |
| `update-rc.d [service_name] start <runlevels>` | (SysV init) Enable service in specific runlevels at boot. |
| `chkconfig [service_name] on/off`              | (SysV init) Enable/disable service for all runlevels.     |

## <mark style="color:red;">Upstart (rarely used now)</mark>

| Command                             | Description       |
| ----------------------------------- | ----------------- |
| `start/stop/restart [service_name]` | Service commands. |
| `initctl start [service_name]`      | Starts a service. |
| `initctl stop [service_name]`       | Stops a service.  |
