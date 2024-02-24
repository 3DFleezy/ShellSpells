# Modify

## <mark style="color:red;">Writing SysV Init Scripts</mark>

### <mark style="color:purple;">Step 1: Create the Script</mark>

Open your text editor and create a new file. For this example, let's call it myservice. \
Start with the shebang line to specify the script interpreter, usually /bin/bash or /bin/sh: \
Add a description, using comments, about the service and how to use the script.

### <mark style="color:purple;">Step 2: Implement Start, Stop, and Other Actions</mark>

SysV init scripts must handle at least the start, stop, and restart actions. It's also good practice to include status and potentially reload if applicable.

Here's a simple template:

```
### BEGIN INIT INFO
# Provides:          myservice
# Required-Start:    $local_fs $network $named $time $syslog
# Required-Stop:     $local_fs $network $named $time $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Description:       A simple script to manage myservice
### END INIT INFO

case "$1" in
    start)
        echo "Starting myservice"
        # Command to start your service, e.g.:
        /path/to/myservice start
        ;;
    stop)
        echo "Stopping myservice"
        # Command to stop your service, e.g.:
        /path/to/myservice stop
        ;;
    restart)
        $0 stop
        $0 start
        ;;
    status)
        # Command to check status of your service, e.g.:
        /path/to/myservice status
        ;;
    *)
        echo "Usage: $0 {start|stop|restart|status}"
        exit 1
        ;;
esac

exit 0
```

### <mark style="color:purple;">Step 3: Make the Script Executable</mark>

Save your script in /etc/init.d/myservice (replace myservice with your service's name). Make it executable by running:\
`sudo chmod +x /etc/init.d/myservice`

### <mark style="color:purple;">Step 4: Test Your Script</mark>

Test your script to ensure it properly starts, stops, restarts, and reports the status of your service: \
`sudo /etc/init.d/myservice start`\
`sudo /etc/init.d/myservice stop`\
`sudo /etc/init.d/myservice restart`\
`sudo /etc/init.d/myservice status`

### <mark style="color:purple;">Step 5: Enable the Service for Automatic Startup (Optional)</mark>

If you want your service to start automatically at boot, you need to add symbolic links to your script in the appropriate /etc/rc?.d/ directories. You can use the update-rc.d command for this purpose:\
`sudo update-rc.d myservice defaults`

This command will create the necessary links based on the Default-Start and Default-Stop values specified in the init script header.

Note:

The `### BEGIN INIT INFO` section at the top of the script provides metadata for dependency-based boot sequencing. Adjust Required-Start, Required-Stop, Default-Start, and Default-Stop as needed for your service.

Remember to replace `/path/to/myservice` with the actual command or script used to start, stop, and check the status of your service. \
This basic template should be customized to fit the specific needs of the service you're managing.

## <mark style="color:red;">Writing SystemD Scripts</mark>

### <mark style="color:purple;">Step 1: Create the Service Unit File</mark>

Open your text editor to create a new file with the .service extension. \
For this example, we'll name the file myservice.service. \
Define the service unit by specifying directives under \[Unit], \[Service], and \[Install] sections.&#x20;

Here's a basic template:

```
[Unit]
Description=My Custom Service
After=network.target

[Service]
Type=simple
ExecStart=/path/to/your/application
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

`Description`- gives a human-readable description of the service. \
`After`- specifies the order in which services are started. network.target is common for services that require network access. \
`Type`- defines the startup behavior of the service. simple is the default, where systemd considers the service started immediately after the ExecStart process is forked.\
`ExecStart`- specifies the command to start the service. Replace /path/to/your/application with the actual command. \
`Restart`- defines the service restart policy. on-failure means the service will be restarted when it exits with a non-zero exit code. \
`WantedBy`- determines where the service is installed if enabled. multi-user.target is a common target for services that should start in a multi-user system runlevel.

### <mark style="color:purple;">Step 2: Save and Store the Unit File</mark>

Save your file with the .service extension. Store the unit file in /etc/systemd/system/. The path for the unit file will be /etc/systemd/system/myservice.service. You might need root permissions to save files in this directory.\
`sudo cp myservice.service /etc/systemd/system/myservice.service`

### <mark style="color:purple;">Step 3: Reload systemd, Enable and Start the Service</mark>

After saving your service file, you need to tell systemd about the new service and optionally enable it to start at boot.

Reload systemd to read the new service file:\
`sudo systemctl daemon-reload`

Enable the service to start on boot:\
`sudo systemctl enable myservice.service`

Start the service now without rebooting:\
`sudo systemctl start myservice.service`

### <mark style="color:purple;">Step 4: Verify the Service Status</mark>

You can check the status of your service to ensure it's running correctly:\
`sudo systemctl status myservice.service`

#### <mark style="color:green;">Additional Notes</mark>

Modify the ExecStart, and potentially add ExecStop and ExecReload, to manage how your service starts, stops, and reloads. Adjust the \[Unit] section to specify dependencies and ordering to other units with Requires, Wants, and Before or After. For complex services, you might also need to set environment variables using Environment or EnvironmentFile directives in the \[Service] section.

## <mark style="color:red;">Writing Upstart Scripts</mark>

When writing Upstart job files, you define jobs using stanzas that specify how and when a job should start or stop. These stanzas include:

`start on` Specifies the event that causes the job to start.\
`stop on` Specifies the event that causes the job to stop. \
`script ...` end script or exec: Used to define the command or script to run.

Example of starting a service:

```
# /etc/init/myservice.conf
description "My Service"
start on filesystem and started networking
stop on shutdown

exec /usr/local/bin/myservice
```

This configuration starts myservice when the filesystem and networking are ready and stops it on system shutdown. The exec stanza directly runs the command specified.
