# Examples

## <mark style="color:red;">Emails</mark>

Matches valid email addresses.

```bash
^(?:[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,})$
```

Another pattern to match valid email addresses.

```bash
^\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b$
```

Yet another pattern to match valid email addresses.

```bash
^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$
```

## <mark style="color:red;">URLs</mark>

Matches URLs with optional protocol and subdomains.

```bash
^(?:https?://)?(?:www\.)?[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}(?:/\S*)?$
```

Another pattern to match URLs.

```bash
^(https?|ftp):\/\/[^\s/$.?#].[^\s]*$ 
```

Yet another pattern to match URLs.

```bash
^(https?|ftp):\/\/[a-zA-Z0-9]+\.[a-zA-Z0-9]+\.[a-zA-Z0-9]+\.[a-zA-Z0-9]+\/[^\s]*$
```

## <mark style="color:red;">Numbers (with and without decimals)</mark>

Matches numbers with optional sign and decimal points.

```bash
^-?\d+\.?\d*$
```

Another pattern to match numbers.

```bash
^-?\d+(\.\d+)?$
```

Yet another pattern to match numbers.

```bash
^-?[0-9]+(\.[0-9]+)?$
```

## <mark style="color:red;">Dates of all known formats</mark>

Matches dates in various formats.

{% code overflow="wrap" %}
```bash
^(?:(?:0?[1-9]|1[0-2])[-\/.](?:0?[1-9]|[12]\d|3[01])[-\/.]\d{4})|(?:(?:0?[1-9]|[12]\d|3[01])[-\/.](?:0?[1-9]|1[0-2])[-\/.]\d{4})|(?:(?:0?[1-9]|1[0-2])[-\/.]\d{1,2}[-\/.]\d{2,4})$
```
{% endcode %}

Another pattern to match dates.

```bash
^(0[1-9]|1[012])[- /.](0[1-9]|[12][0-9]|3[01])[- /.](19|20)\d\d$
```

Yet another pattern to match dates.

```bash
^(19|20)\d\d[- /.](0[1-9]|1[012])[- /.](0[1-9]|[12][0-9]|3[01])$
```

## <mark style="color:red;">Time in all known formats</mark>

Matches time in various formats.

```bash
^(?:0?[1-9]|1[0-2]):(?:[0-5]\d)(?::(?:[0-5]\d))?(?:\s?[APap][mM])?$
```

Another pattern to match time.

```bash
^([01]?[0-9]|2[0-3]):[0-5][0-9](:[0-5][0-9])?$
```

Yet another pattern to match time.

```bash
^(0[0-9]|1[0-9]|2[0-3]):([0-5][0-9])(:[0-5][0-9])?$
```

## <mark style="color:red;">Phone Numbers</mark>

Matches US phone numbers with optional area code and formatting.

```bash
^(?:\+?1[-. ]?)?\(?[2-9][0-9]{2}\)?[-. ]?[2-9][0-9]{2}[-. ]?\d{4}$
```

Another pattern to match phone numbers.

```bash
^(\+\d{1,2}\s?)?((\(\d{3}\))|\d{3})([\s.-]?)\d{3}([\s.-]?)\d{4}$
```

Yet another pattern to match phone numbers.

```bash
^([+]?[0-9]{1,2}[.-\s]?)?(\([0-9]{3}\)|[0-9]{3})[.-\s]?[0-9]{3}[.-\s]?[0-9]{4}$
```

## <mark style="color:red;">Zip Codes</mark>

Matches US zip codes in various formats.

```bash
^\d{5}(?:-\d{4})?$
```

Another pattern to match US zip codes.

```bash
^\d{5}-\d{4}(?:\d{2})?$
```

Yet another pattern to match US zip codes.

```bash
^\d{5}(?:-\d{4})?$
```

## <mark style="color:red;">Password Strength validation</mark>

Matches passwords with at least 8 characters, containing at least one uppercase letter, one lowercase letter, one number, and one special character.

```bash
^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$
```

Another pattern for password validation.

```bash
^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[a-zA-Z]).{8,}$
```

Yet another pattern for password validation.

```bash
^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%^&+=]).*$
```

## <mark style="color:red;">File Extensions</mark>

Matches file extensions (e.g., .txt, .jpg, .pdf).

```bash
\.\w+$
```

Another pattern to match file extensions.

```bash
\.(?:jpg|gif|png|pdf|)$
```

## <mark style="color:red;">IPv4 Addresses</mark>

Matches IPv4 addresses in dotted decimal notation.

```bash
^(?:\d{1,3}\.){3}\d{1,3}$
```

Another pattern to match IPv4 addresses.

{% code overflow="wrap" %}
```bash
^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$
```
{% endcode %}

## <mark style="color:red;">Credit Card Numbers</mark>

Matches credit card numbers in various formats.

{% code overflow="wrap" %}
```bash
^(?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14}|3[47][0-9]{13}|6(?:011|5[0-9]{2})[0-9]{12})$
```
{% endcode %}

Another pattern to match credit card numbers.

```bash
^(?:\d[ -]*?){13,16}$
```

## <mark style="color:red;">City, State Abbreviations</mark>

Matches US city names followed by state abbreviations.

```bash
^[a-zA-Z\s]+,\s*[A-Z]{2}$
```

Another pattern to match city names and state abbreviations.

```bash
^[a-zA-Z\s]+,\s*[A-Z]{2}$
```

## <mark style="color:red;">Social Security Numbers</mark>

Matches US social security numbers in various formats.

```bash
^(?!000|666|9\d{2})\d{3}-(?!00)\d{2}-(?!0000)\d{4}$
```

Another pattern to match social security numbers.

```bash
^\d{3}-\d{2}-\d{4}$
```

## <mark style="color:red;">Dollar Amounts</mark>

Matches dollar amounts in various formats.

```bash
^\$?\d{1,3}(?:,?\d{3})*(?:\.\d{2})?$
```

Another pattern to match dollar amounts.

```bash
^\$[0-9]+(\.[0-9]{2})?$
```

## <mark style="color:red;">Hexadecimal Values</mark>

Matches hexadecimal values.

```bash
^(?:0[xX])?[0-9a-fA-F]+$
```

Another pattern to match hexadecimal values.

```bash
^#?([a-f0-9]{6}|[a-f0-9]{3})$
```

## <mark style="color:red;">MAC Addresses</mark>

Matches MAC addresses in various formats.

```bash
^(?:[0-9a-fA-F]{2}[:-]){5}[0-9a-fA-F]{2}$
```

Another pattern to match MAC addresses.

```bash
^([0-9A-Fa-f]{2}[:-]){5}([0-9A-Fa-f]{2})$
```

## <mark style="color:red;">HTML Tags</mark>

Matches HTML tags.

```bash
<[^>]*>
```

Another pattern to match HTML tags.

```bash
<[a-zA-Z][^>]*>
```
