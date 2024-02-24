# Encode/Decode

## <mark style="color:red;">Encode</mark>

### <mark style="color:purple;">Base64</mark>

Encode in base64.

```bash
base64 [file]
```

Encode in base64 without wrapping lines.

The `-w` option specifies line wrap, and `0` disables it (GNU base64):

```bash
base64 -w 0 [file]
```

### <mark style="color:purple;">URL</mark>

Use Perl's URI::Escape module to URL-encode "string":

```bash
perl -MURI::Escape -e 'print uri_escape($ARGV[0]);' "string"
```

Use `curl` to URL-encode "string".

Sends a dummy request to `curl` and extracts the encoded URL part:

```bash
echo -n "string" | curl -Gso /dev/null -w %{url_effective} --data-urlencode @- "" | cut -c 3-
```

### <mark style="color:purple;">Hex</mark>

Create a hex dump of a file in a plain hex format using `xxd`.

This format is easy to use in scripts for further processing:

```bash
xxd -p [file]
```

Use `od` (octal dump) to output the file content in hexadecimal.

The `cut` command is used to trim the output to show only the hex values:

```bash
od -t x1 [file] | cut -c8- 
```

### <mark style="color:purple;">Character Set Conversion</mark>

Convert the character encoding of a file. `-f` specifies the original encoding, and `-t` specifies the target encoding.

```bash
iconv -f from_encoding -t to_encoding [file]
```

### <mark style="color:purple;">MIME Encoding</mark>

These commands might not be available in all distributions and are part of the mailutils or similar packages

Encode a file using MIME base64 encoding. This command is part of some older or specific utilities for handling email data:

```bash
mimencode [file]
```

Another tool for MIME base64 encoding. Similar in function to `mimencode`, but availability varies by system:

```bash
mmencode [file]
```

### <mark style="color:purple;">Reverse</mark>

Reverse content

```bash
tac [file] > [newfile]
```

## <mark style="color:red;">Decode</mark>

### <mark style="color:purple;">Base64</mark>

Decode a base64-encoded file. The `-d` option specifies decoding (use `-D` on macOS):

```bash
base64 -d [file]
```

### <mark style="color:purple;">URL</mark>

Use Perl's URI::Escape module to URL-decode "encoded\_string":

```bash
perl -MURI::Escape -e 'print uri_unescape($ARGV[0]);' "encoded_string"
```

### <mark style="color:purple;">Hex</mark>

Reverse (decode) a plain hex dump back into binary.

Use `-r` with `xxd` to revert a hex dump back to its original binary form:

```bash
xxd -p -r [file]
```

### <mark style="color:purple;">Character Set Conversion</mark>

Convert the character encoding of a file back to the desired encoding.

The process is the same as encoding, just reverse the `-f` (from) and `-t` (to) encodings as needed:

```bash
iconv -f from_encoding -t to_encoding [file]
```

### <mark style="color:purple;">MIME Encoding</mark>

If you used mimencode or mmencode for MIME base64 encoding, you might need to find an alternative for decoding since direct counterparts for decoding might not be explicitly named or available.

For MIME base64 decoding, you can use `base64 -d` or consider Perl solutions:

Decode a MIME base64-encoded file, assuming the content is base64 and does not include MIME headers:

```bash
base64 -d [file]
```

### <mark style="color:purple;">Reverse</mark>

Reverse content

```bash
tac [file] > <newfile>
```
