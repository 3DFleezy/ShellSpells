# Process I/O Redirection

<table data-header-hidden><thead><tr><th width="198">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>> filename</code></td><td>Redirects standard output to a file.</td></tr><tr><td><mark style="color:yellow;"><code>>> filename</code></td><td>Appends standard output to a file.</td></tr><tr><td><mark style="color:yellow;"><code>&#x3C; filename</code></td><td>Redirects standard input from a file.</td></tr><tr><td><mark style="color:yellow;"><code>2> filename</code></td><td>Redirects standard error to a file.</td></tr><tr><td><mark style="color:yellow;"><code>&#x26;> filename</code></td><td>Redirects both standard output and error to a file.</td></tr></tbody></table>

## <mark style="color:red;">& - Running Command in Background</mark>&#x20;

Use the `&` to do this.

For example, if you want to copy a large file, you can use this to keep the terminal free while a long task takes place.

## <mark style="color:red;">&& - Stringing Commands</mark>&#x20;

The `&&` lets you run multiple commands in the same line

{% hint style="success" %}
The previous command has to successfully run or the following commands will not execute.
{% endhint %}
