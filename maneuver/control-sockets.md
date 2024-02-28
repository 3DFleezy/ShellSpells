# Control Sockets

## <mark style="color:red;">Notes</mark>

Benefits:

<mark style="color:orange;">**Multiplexing**</mark> - Create more than one connection through an already established secure channel

<mark style="color:orange;">**Data exfiltration**</mark> - Downloading through an already established secure connection

<mark style="color:orange;">**Less logging**</mark> - Creates a special type of log file (socket file) that shows you are already logged in to the SSH Server. As long as that PID (window is open) stays alive, you can open as many new sessions to that server as you want because you are already pre-authenticated.

{% hint style="info" %}
Only the first connection where the control socket was created and is the only connection that has a respective established connection and authentication log entry.
{% endhint %}

{% hint style="warning" %}
As long as each connection comes from the same source system, no further connections or authentication log entries will be generated on the remote system.
{% endhint %}

## <mark style="color:red;">Control Sockets (config)</mark>

Two main ways to configure:

### <mark style="color:purple;">Command Line Method</mark>

```bash
ssh -M -S /tmp/s root@<ip> <-R or -L>
ssh -S /tmp/s user@<ip>
scp -o 'ControlPath=/tmp/s' user@<ip>:<Path>
```

### <mark style="color:purple;">Configuration File Method (\~/.ssh/ssh\_config)</mark>

HostName \*

ControlPath \~/.ssh/controlmasters/%r@%h:%p

ControlMaster auto

ControlPersist 10m

## <mark style="color:red;">Manipulate SSH Config for Master Control Socket</mark>

### <mark style="color:purple;">Making SSH Control Sockets Persistent</mark>

Configure the following settings in either or both the

system-wide config \*\* /etc/ssh/ssh\_config

per-user config \*\* \~/.ssh/config,

The per-user config file will take precedence over the system wide SSH client configuration file.

If you are using control sockets to specific systems, create entries for each host:

HostName host.example.org

ControlPath \~/.ssh/controlmasters/%r@%h:%p

ControlMaster auto

ControlPersist 10m

The socket is created in the "\~/.ssh/controlsmasters/" and is named user@host:port

<mark style="color:orange;">**%r**</mark> - remote user name

<mark style="color:orange;">**%h**</mark> - remote host name

<mark style="color:orange;">**%p**</mark> - remote port

ControlMaster accepts five different values:

<mark style="color:orange;">**`no`**</mark> (default) New sessions will not try to connect to an established master session, but additional sessions can still multiplex by connecting explicitly to an existing socket.

<mark style="color:orange;">**`yes`**</mark> Creates a new master session each time, unless overridden. The new master session will listen for connections.

<mark style="color:orange;">**`ask`**</mark> Creates a new master session each time, unless overridden, which listens for connections.\
If overridden, ssh-askpass(1) will ask the master session owner to approve or deny the request.\
If the request is denied, then the session being created falls back to being a regular, standalone session.

<mark style="color:orange;">**`auto`**</mark> Creates a master session automatically but if there is a master session already available, subsequent sessions are automatically multiplexed.

<mark style="color:orange;">**`autoask`**</mark> Automatically assumes that if a master session exists, that subsequent sessions should be multiplexed, but asks first before adding a session.

Refused connections are logged to the master session.

<mark style="color:orange;">**`ControlPersist`**</mark> specifies whether to keep the control socket active when idle, or for how long.

The options are 'yes', 'no' or a time interval.

If a 'time interval' is given, the default is in seconds. Units can extend the time to minutes, hours, days, weeks or a combination.

If 'yes' the master connection stays in the background indefinitely.

To make SSH user control sockets for all SSH connections, a wildcard can be specified with the Host option:

Host \*

ControlMaster auto

ControlPath \~/.ssh/cm\_socket/%r@%h:%p

```bash
` mkdir ~/.ssh/cm_socket
```
