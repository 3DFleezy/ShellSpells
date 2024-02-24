# Hidden Files

{% hint style="info" %}
NOTE: By default, `find` ignores hidden files/dirs unless you use `-a`.
{% endhint %}

| Command                                                       | Description             |
| ------------------------------------------------------------- | ----------------------- |
| `ls -a`                                                       | List all files          |
| `find / -type f -name ".*"`                                   | Find hidden files       |
| `find / -type f -name ".*" -exec ls -l {} \;`                 | Find hidden files       |
| `find / -type f -name ".*" -exec ls -latriQ {} 2>/dev/null +` | Find hidden files       |
| `find / -type d -name ".*"`                                   | Find hidden directories |
| `find / -type d -name ".*" -exec ls -ld {} \;`                | Find hidden directories |
| `find / -type d -name ".*" -exec ls -ladtri {} 2>/dev/null +` | Find hidden directories |
