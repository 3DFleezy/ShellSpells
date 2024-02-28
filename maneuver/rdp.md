# RDP

## <mark style="color:red;">xfreerdp</mark>

{% code overflow="wrap" %}
```bash
xfreerdp /u:user /p:'pa$$word' /cert:ignore /v:<Win_IP> /dynamic-resolution +clipboard
```
{% endcode %}

{% hint style="warning" %}
Make sure to put the password in 'single quotes'!
{% endhint %}

### <mark style="color:purple;">From a Tunnel:</mark>

From local tunnel to windows with RDP:

```bash
ssh user@<localhost> -L 1111:<target_ip>:3389
```

From Localhost:

```bash
xfreerdp /u:user /v:localhost:12345 /dynamic-resolution +clipboard
```
