# Create a Service

## <mark style="color:red;">Systemd</mark>

Systemd services are defined in unit files with the .service extension. \
Here's a basic structure:

```
[Unit]
Description=Your service description
After=network.target

[Service]
Type=simple
User=your_username
WorkingDirectory=/path/to/service/directory
ExecStart=/path/to/service/executable

[Install]
WantedBy=multi-user.target
```

Replace placeholders: \
Description: Short description of your service. \
After: Specify dependencies (e.g., network services). \
User: User running the service. \
WorkingDirectory: Service's working directory. \
ExecStart: Path to the service executable. \
WantedBy: Target unit to enable automatic startup.

Save the file: \
Save it as \[service\_name].service in /etc/systemd/system/.

Reload and enable:

```bash
sudo systemctl daemon-reload
```

```bash
sudo systemctl enable <service_name>.service
```

Start the service:

```bash
sudo systemctl start <service_name>.service.
```

## <mark style="color:red;">SysV</mark>&#x20;

SysV services are typically shell scripts located in /etc/init.d/. \
Here's a basic example:

```
#!/bin/bash

start() {
  # Start your service here
  /path/to/service/executable &
}

stop() {
  # Stop your service here
  pkill -f /path/to/service/executable
}

case "$1" in
  start)
    start
    ;;
  stop)
    stop
    ;;
  *)
    echo "Usage: $0 {start|stop}"
    exit 1
    ;;
esac

exit 0
```

Make the script executable:

```bash
chmod +x /etc/init.d/<service_name>
```

Start/stop the service:

```bash
/etc/init.d/<service_name> start/stop
```

Optional: Enable automatic startup by linking the script to /etc/rc?.d/S (depending on your runlevel).

## <mark style="color:red;">Upstart</mark>

Upstart uses job files with the .conf extension usually located in /etc/init.

Here's a basic example:

```
description "Your service description"

start on started network-interfaces
script
  # Start your service here
  /path/to/service/executable &
end script

pre-stop script
  # Stop your service here
  pkill -f /path/to/service/executable
end script
```

Save the file: Save it as \[service\_name].conf in /etc/init/.

Reload and start:

```bash
sudo initctl reload 
```

```bash
sudo start <service_name>
```
