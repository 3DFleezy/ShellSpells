# Encode/Decode

## certutil

Encode/decode files using Base64 or hexadecimal formats.

```powershell
certutil -encode <input_file> <output_file>
```

```powershell
certutil -decode <input_file> <output_file>
```

## cipher

Encrypt/decrypt files using built-in Windows encryption.

```powershell
cipher /e <input_file> [/a] [/s:<password>]
```

```powershell
cipher /d <input_file> [/a] [/s:<password>]
```

## System.Text Namespace

Invoking the System.Text Namespace, Encoding Class, and GetByte:

```powershell
[System.Text.Encoding]::GetBytes()
```

## UTF8

Writes output to a file, with options for specifying encoding:

```powershell
Out-File -FilePath C:\path\to\file.txt -InputObject "Text to add" -Encoding UTF8 
```

## Base64

Decode Base64-encoded strings or files.

```powershell
ConvertFrom-Base64 -InputObject <encoded_data>
```

Encode data into Base64 format.

```powershell
ConvertTo-Base64 -InputObject <data_to_encode>
```

Base64 encode a string:

```powershell
[Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes("encoded text"))
```

Base64 decode a string:

```powershell
[System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String("encoded text"))
```

Base64 decode:

{% code overflow="wrap" %}
```powershell
[System.Convert]::ToBase64String([System .Text.Encoding]::UTF8.GetBytes("Text to encode"))
```
{% endcode %}

Base64 encode a file:

```powershell
[Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\path\to\inputfile"))
```

Base64 decode a string to a file:

{% code overflow="wrap" %}
```powershell
[System.IO.File]::WriteAllBytes("C:\path\to\outputfile", [Convert]::FromBase64String("Base64EncodedString"))
```
{% endcode %}

## Unicode Array

Converts the text into a Unicode Array using .NET API:

\`(\[System.Text.Encoding]::Unicode.GetBytes("encoded text"))

## URL Encoding

URL encode a string:

```powershell
[System.Web.HttpUtility]::UrlEncode("encoded text")
```

URL decode a string:

```powershell
[System.Web.HttpUtility]::UrlDecode("encoded text")
```

### HTML Encoding

HTML encode a string:

```powershell
[System.Web.HttpUtility]::HtmlEncode("encoded text")
```

HTML decode a string:

```powershell
[System.Web.HttpUtility]::HtmlDecode("encoded text")
```
