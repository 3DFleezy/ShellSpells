# Hidden Files

{% hint style="info" %}
NOTE: By default, `find` ignores hidden files/dirs unless you use `-a`.
{% endhint %}

<table data-header-hidden data-full-width="true"><thead><tr><th width="628">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>ls -a</code></td><td>List all files</td></tr><tr><td><mark style="color:yellow;"><code>find / -type f -name ".*"</code></td><td>Find hidden files</td></tr><tr><td><mark style="color:yellow;"><code>find / -type f -name ".*" -exec ls -l {} \;</code></td><td>Find hidden files</td></tr><tr><td><mark style="color:yellow;"><code>find / -type f -name ".*" -exec ls -latriQ {} 2>/dev/null +</code></td><td>Find hidden files</td></tr><tr><td><mark style="color:yellow;"><code>find / -type d -name ".*"</code></td><td>Find hidden directories</td></tr><tr><td><mark style="color:yellow;"><code>find / -type d -name ".*" -exec ls -ld {} \;</code></td><td>Find hidden directories</td></tr><tr><td><mark style="color:yellow;"><code>find / -type d -name ".*" -exec ls -ladtri {} 2>/dev/null +</code></td><td>Find hidden directories</td></tr></tbody></table>
