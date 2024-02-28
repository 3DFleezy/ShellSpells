# Alternate Methods

## <mark style="color:red;">/dev/tcp</mark>

### <mark style="color:purple;">File Transfer</mark>

Client (sending)

```bash
cat file.txt > /dev/tcp/10.10.10.1/1111
```

Listener (receiving)

```bash
nc -l -p 1111 > file.txt
```

## <mark style="color:red;">/dev/udp</mark>

/dev/udp is like the /dev/tcp except to interact with the udp stack.

## <mark style="color:red;">OpenSSL</mark>

Erick Veil has a great write up on this. See the link here.

https://erickveil.github.io/openssl,/ssl,/encryption,/socket,/network,/bash,/linux/2021/01/21/How-to-Send-Encrypted-Messages-Using-OpenSSL-on-the-Command-Line.html

Connect to localhost:

```bash
openssl s_client -connect 127.0.0.1:30001
```

## <mark style="color:red;">Ncat</mark>

### <mark style="color:purple;">Encrypted Transfer</mark>

```bash
ncat --ssl <ip> <port> < <file>
```

### <mark style="color:purple;">Ncat Options</mark>

<mark style="color:yellow;">`-c`</mark> (--sh-exec) \[] = Executes the given command via /bin/sh

<mark style="color:yellow;">`-e`</mark> (--exec) \[] = Executes the given command

<mark style="color:yellow;">`-k`</mark> (--keep-open) = To keep TCP port open for other connections.

<mark style="color:yellow;">`-l`</mark> (--listen) = Bind and listen for incoming connections

<mark style="color:yellow;">`-t`</mark> (--telnet) = Answer Telnet negotiations

<mark style="color:yellow;">`-u`</mark> (--udp) = use UDP (TCP default). Cannot be used with --keep-open.

<mark style="color:yellow;">`-v`</mark> (--verbose) = Set verbosity level (can be used several times)

<mark style="color:yellow;">`-w`</mark> (--wait) = Connect timeout

<mark style="color:yellow;">`-z`</mark> = Zero-I/O mode, report connection status only

<mark style="color:yellow;">`--chat`</mark> = Start a simple Ncat chat server

<mark style="color:yellow;">`--sctp`</mark> = SCTP, the Stream Control Transmission Protocol, is a newer reliable protocol. Ncat uses a TCP-compatible subset of SCTP features, not including multiple streams per connection or message boundaries. SCTP may be combined with SSL.

<mark style="color:yellow;">`--ssl`</mark> = Connect or listen with SSL. Works with TCP or SCTP.
