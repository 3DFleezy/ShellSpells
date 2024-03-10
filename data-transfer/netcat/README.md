# Netcat

## <mark style="color:red;">Chat</mark>

```bash
Client (initiating)		Listener (receiving)
nc 10.0.0.2 1234 ------> nc -lp 1234
```

## <mark style="color:red;">File Content Transfer</mark>

```bash
Client (sending)		    Listener (receiving)
nc 10.0.0.2 1234 < file.txt ------> nc -lp 1234 > file.txt

Listener (sending)	       Client (receiving)
nc -lp 1234 < file.txt ------> nc 10.0.0.1 1234 > file.txt
```

## <mark style="color:red;">Send Text</mark>

Can send text too (this example is sent to localhost):

```bash
echo "text" | nc localhost 10000
```

## <mark style="color:red;">Using SSH Tunnels (Edit this)</mark>

Listener (sending)

```bash
nc -l -p 9876 < file.txt
```

Receiver

```bash
ssh -L 1111:10.0.0.3:22 user1@10.0.0.2 -NT
ssh -L 2222:10.0.0.4:9876 -p 1111 user2@localhost -NT
nc localhost 2222 > file.txt
```



