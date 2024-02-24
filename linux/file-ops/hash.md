# Hash

<table data-header-hidden><thead><tr><th width="343">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>md5sum [file]</code></td><td>MD5 hash.</td></tr><tr><td><code>sha1sum [file]</code></td><td>SHA-1 hash.</td></tr><tr><td><code>sha256sum [file]</code></td><td>SHA-256 hash.</td></tr><tr><td><code>sha512sum [file]</code></td><td>SHA-512 hash.</td></tr><tr><td><code>sha224sum [file]</code></td><td>SHA-224 hash.</td></tr><tr><td><code>sha384sum [file]</code></td><td>SHA-384 hash.</td></tr><tr><td><code>cksum [file]</code></td><td>CRC checksum along with the byte size.</td></tr><tr><td><code>openssl md5 [file]</code></td><td>MD5 hash using OpenSSL.</td></tr><tr><td><code>openssl sha1 [file]</code></td><td>SHA-1 hash using OpenSSL.</td></tr><tr><td><code>openssl dgst -sha256 [file]</code></td><td>SHA-256 hash using OpenSSL.</td></tr><tr><td><code>openssl dgst -sha512 [file]</code></td><td>SHA-512 hash using OpenSSL.</td></tr></tbody></table>

Compare two files by their SHA256 hash: If the output is 1, it indicates that the two files have the same SHA-256 hash.

{% hint style="info" %}
This is complete overkill...
{% endhint %}

{% code overflow="wrap" %}
```bash
echo "$(sha256sum file1 | cut -d' ' -f1) $(sha256sum file2 | cut -d' ' -f1)" | tr ' ' '\n' | uniq | wc -l
```
{% endcode %}
