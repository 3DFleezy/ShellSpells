# Encode/Decode

## Encode

### Base64

Encode in base64.

```bash
base64 [file]
```

Encode in base64 without wrapping lines.

The `-w` option specifies line wrap, and `0` disables it (GNU base64):

```bash
base64 -w 0 [file]
```

### URL

Use Perl's URI::Escape module to URL-encode "string":

```bash
perl -MURI::Escape -e 'print uri_escape($ARGV[0]);' "string"
```

Use `curl` to URL-encode "string".

Sends a dummy request to `curl` and extracts the encoded URL part:

```bash
echo -n "string" | curl -Gso /dev/null -w %{url_effective} --data-urlencode @- "" | cut -c 3-
```

### Hex

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

### Character Set Conversion

Convert the character encoding of a file. `-f` specifies the original encoding, and `-t` specifies the target encoding.

```bash
iconv -f from_encoding -t to_encoding [file]
```

### MIME Encoding

These commands might not be available in all distributions and are part of the mailutils or similar packages

Encode a file using MIME base64 encoding. This command is part of some older or specific utilities for handling email data:

```bash
mimencode [file]
```

Another tool for MIME base64 encoding. Similar in function to `mimencode`, but availability varies by system:

```bash
mmencode [file]
```

### Reverse

Reverse content

```bash
tac [file] > [newfile]
```

## Decode

### Base64

Decode a base64-encoded file. The `-d` option specifies decoding (use `-D` on macOS):

```bash
base64 -d [file]
```

### URL

Use Perl's URI::Escape module to URL-decode "encoded\_string":

```bash
perl -MURI::Escape -e 'print uri_unescape($ARGV[0]);' "encoded_string"
```

### Hex

Reverse (decode) a plain hex dump back into binary.

Use `-r` with `xxd` to revert a hex dump back to its original binary form:

```bash
xxd -p -r [file]
```

### Character Set Conversion

Convert the character encoding of a file back to the desired encoding.

The process is the same as encoding, just reverse the `-f` (from) and `-t` (to) encodings as needed:

```bash
iconv -f from_encoding -t to_encoding [file]
```

### MIME Encoding

If you used mimencode or mmencode for MIME base64 encoding, you might need to find an alternative for decoding since direct counterparts for decoding might not be explicitly named or available.

For MIME base64 decoding, you can use `base64 -d` or consider Perl solutions:

Decode a MIME base64-encoded file, assuming the content is base64 and does not include MIME headers:

```bash
base64 -d [file]
```

### Reverse

Reverse content

```bash
tac [file] > <newfile>
```
