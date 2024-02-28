# Windows Port Proxy

Syntax:

{% code overflow="wrap" %}
```bash
netsh interface portproxy add v4tov4 listenport=<LocalPort> listenaddress=<LocalIP> connectport=<TargetPort> connectaddress=<TargetIP> protocol=tcp
```
{% endcode %}

Example:

{% code overflow="wrap" %}
```bash
netsh interface portproxy add v4tov4 listenport=1111 listenaddress=192.168.1.10 connectport=80 connectaddress=192.168.0.33 protocol=tcp
```
{% endcode %}

View the PortProxy:

```bash
netsh interface portproxy show all
```

Delete the PortProxy:

```bash
netsh interface portproxy delete v4tov4 listenport=<LocalPort>
```

Delete all PortProxies set up:

```bash
netsh interface portproxy reset
```
