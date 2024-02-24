# Hash

| Command                       | Description                            |
| ----------------------------- | -------------------------------------- |
| `md5sum [file]`               | MD5 hash.                              |
| `sha1sum [file]`              | SHA-1 hash.                            |
| `sha256sum [file]`            | SHA-256 hash.                          |
| `sha512sum [file]`            | SHA-512 hash.                          |
| `sha224sum [file]`            | SHA-224 hash.                          |
| `sha384sum [file]`            | SHA-384 hash.                          |
| `cksum [file]`                | CRC checksum along with the byte size. |
| `openssl md5 [file]`          | MD5 hash using OpenSSL.                |
| `openssl sha1 [file]`         | SHA-1 hash using OpenSSL.              |
| `openssl dgst -sha256 [file]` | SHA-256 hash using OpenSSL.            |
| `openssl dgst -sha512 [file]` | SHA-512 hash using OpenSSL.            |

Compare two files by their SHA256 hash: If the output is 1, it indicates that the two files have the same SHA-256 hash.

{% hint style="info" %}
This is complete overkill...
{% endhint %}

{% code overflow="wrap" %}
```bash
echo "$(sha256sum file1 | cut -d' ' -f1) $(sha256sum file2 | cut -d' ' -f1)" | tr ' ' '\n' | uniq | wc -l
```
{% endcode %}
