# Process I/O Redirection

| Command       | Description                                         |
| ------------- | --------------------------------------------------- |
| `> filename`  | Redirects standard output to a file.                |
| `>> filename` | Appends standard output to a file.                  |
| `< filename`  | Redirects standard input from a file.               |
| `2> filename` | Redirects standard error to a file.                 |
| `&> filename` | Redirects both standard output and error to a file. |

## <mark style="color:red;">& - Running Command in Background</mark>&#x20;

Use the `&` to do this.

For example, if you want to copy a large file, you can use this to keep the terminal free while a long task takes place.

## <mark style="color:red;">&& - Stringing Commands</mark>&#x20;

The `&&` lets you run multiple commands in the same line

{% hint style="success" %}
The previous command has to successfully run or the following commands will not execute.
{% endhint %}
