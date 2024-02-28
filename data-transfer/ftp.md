# FTP

## <mark style="color:red;">FTP</mark>

### <mark style="color:red;">Basic Commands</mark>

| <mark style="color:yellow;">`ftp 10.10.10.1`</mark>  | FTP connect           |
| ---------------------------------------------------- | --------------------- |
| <mark style="color:yellow;">`sftp 10.10.10.1`</mark> | SFTP connect          |
| <mark style="color:yellow;">`passive`</mark>         | enter passive mode    |
| <mark style="color:yellow;">`ls`</mark>              | list files            |
| <mark style="color:yellow;">`get file.txt`</mark>    | download file         |
| <mark style="color:yellow;">`exit`</mark>            | terminate ftp session |

You can use wget to download the files of an FTP server:

```bash
wget -r ftp://10.10.0.1
```

### <mark style="color:purple;">FTP Notes</mark>

Uses TCP

Port 21 - Control Connection

Port 21 - Data Connection

Insecure but can be enhanced with SSL/TLS (FTPS)

### <mark style="color:purple;">TFTP Notes</mark>

Trivial File Transfer Protocol

Uses UDP so requires no confirmation that the data was sent.

Insecure

### <mark style="color:purple;">SFTP Notes</mark>

SSH File Transfer Protocol

Uses TCP transport on port 22.

Uses symmetric and asymmetric encryption

Can authenticate with SSH key or username and password

### <mark style="color:purple;">FTPS Notes</mark>

FTP Secure

Uses TCP port 443

Adds SSL/TLS encryption on top of FTP

Can authenticate with a PKI
