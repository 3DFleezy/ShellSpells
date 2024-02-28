# SCP

## <mark style="color:red;">Basic Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="531">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>scp file.txt user@10.10.10.1:</code></mark></td><td>Send file</td></tr><tr><td><mark style="color:yellow;"><code>scp file.txt user@10.10.10.1:/home/moved.txt</code></mark></td><td>Send file</td></tr><tr><td><mark style="color:yellow;"><code>scp user@10.10.10.1:/home/file.txt moved.txt</code></mark></td><td>Pull file</td></tr><tr><td><mark style="color:yellow;"><code>scp user@10.10.10.1:/home/file.txt /home/user</code></mark></td><td>Pull file</td></tr><tr><td><mark style="color:yellow;"><code>scp user@10.10.10.1:file.txt .</code></mark></td><td>Pull file to current dir</td></tr><tr><td><mark style="color:yellow;"><code>scp -3 user@10.10.10.1:file.txt user@10.10.10.2:</code></mark></td><td>Pull file. (-3) will buffer the file thru your localhost.</td></tr></tbody></table>

## <mark style="color:red;">SCP Syntax w/ Alternate SSHD</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>scp -P 1111 user@10.10.10.1:file.txt .</code></mark></td><td>Pull file using alternate SSH port</td></tr><tr><td><mark style="color:yellow;"><code>scp -P 1111 file.txt user@10.10.10.1:</code></mark></td><td>Send file using alternate SSH port</td></tr></tbody></table>

## <mark style="color:red;">SCP Syntax Through a Tunnel</mark>

```bash
ssh user@10.10.10.1 -L 1111:10.10.10.2:22 -NT
```

Pull file through dynamic tunnel:

```bash
ssh user@10.10.10.1 -D 9050 -NT
```

```bash
proxychains scp user@10.10.10.1:file.txt .
```

```bash
proxychains scp file.txt user@10.10.10.1:
```
