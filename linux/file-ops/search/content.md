# Content

Go-to Command:

```bash
grep -IRil "pattern" /path/to/search
```

<mark style="color:yellow;">`-a`</mark> Includes hidden files/dirs.\
<mark style="color:yellow;">`-I`</mark> Ignore binaries (.bin, .jpg, etc)\
<mark style="color:yellow;">`-R`</mark> Recursive + follows all symlinks\
<mark style="color:yellow;">`-i`</mark> Case-insensitive\
<mark style="color:yellow;">`-l`</mark> Shows only filenames with pattern in the content

<table data-header-hidden data-full-width="true"><thead><tr><th width="670">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>grep -IRil "password|passphrase|secret" /path/to/search</code></mark></td><td>Multiple keywords</td></tr><tr><td><mark style="color:yellow;"><code>grep -IRil --include=*.txt "pattern" /path/to/search</code></mark></td><td>File extensions</td></tr><tr><td><mark style="color:yellow;"><code>grep -v "pattern" /path/to/search</code></mark></td><td>Inverse</td></tr><tr><td><mark style="color:yellow;"><code>grep -vE "(pattern1) | (pattern2)" file.txt</code></mark></td><td>Multiple inverse patterns</td></tr><tr><td><mark style="color:yellow;"><code>zgrep -Iil "pattern" /path/to/search</code></mark></td><td>Basic pattern match</td></tr><tr><td><mark style="color:yellow;"><code>zgrep -Iil "pattern1|pattern2|pattern3" /path/to/search</code></mark></td><td>Multiple keywords (Compressed files)</td></tr><tr><td><mark style="color:yellow;"><code>zgrep -Iil --include=*.gz "pattern" /path/to/search</code></mark></td><td>File extensions (Compressed files)</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name "*.gz" -exec zgrep "pattern" {} +</code></mark></td><td>Recursive zgrep</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -exec grep -Iil "pattern" {} + 2>/dev/null</code></mark></td><td>Search the contents of all files for string. Return filenames.</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name "*.java" -exec grep -il 'pattern' {} \;</code></mark></td><td>Ignore case with -i option</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -empty -exec ls -l {} \;</code></mark></td><td>Empty Files</td></tr><tr><td><mark style="color:yellow;"><code>find / -a -type f -name "*.gz" -exec zgrep 'pattern'{} \;</code></mark></td><td>Search for a string in gzip'd files</td></tr></tbody></table>
