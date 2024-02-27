# Compress/Decompress

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>compact /c &#x3C;file_or_folder></code></mark></td><td>Compresses a file or folder.</td></tr><tr><td><mark style="color:yellow;"><code>compact /u &#x3C;file_or_folder></code></mark></td><td>Decompresses a file or folder.</td></tr><tr><td><mark style="color:yellow;"><code>compact /q &#x3C;file_or_folder></code></mark></td><td>Queries the compression status of a file or folder.</td></tr><tr><td><mark style="color:yellow;"><code>expand &#x3C;compressed_file> &#x3C;destination_folder></code></mark></td><td>Decompresses a file using Microsoft's Expand utility.</td></tr></tbody></table>

Compress a folder to a ZIP file:

{% code overflow="wrap" %}
```powershell
Compress-Archive -Path C:\path\to\sourceFolder -DestinationPath C:\path\to\output.zip
```
{% endcode %}

Decompress a ZIP file to a folder:

{% code overflow="wrap" %}
```powershell
Expand-Archive -Path C:\path\to\input.zip -DestinationPath C:\path\to\destinationFolder
```
{% endcode %}

Compress multiple files into a ZIP file:

{% code overflow="wrap" %}
```powershell
Compress-Archive -Path "C:\path\to\file1.txt", "C:\path\to\file2.txt" -DestinationPath C:\path\to\output.zip
```
{% endcode %}

Compress a folder using Windows built-in command (CMD):

{% code overflow="wrap" %}
```powershell
powershell -command "Compress-Archive -Path C:\path\to\sourceFolder -DestinationPath C:\path\to\output.zip"
```
{% endcode %}

Decompress a ZIP file using Windows built-in command (CMD):

{% code overflow="wrap" %}
```powershell
powershell -command "Expand-Archive -Path C:\path\to\input.zip -DestinationPath C:\path\to\destinationFolder"
```
{% endcode %}

Compress a folder to a ZIP file with maximum compression:

{% code overflow="wrap" %}
```powershell
Compress-Archive -Path C:\path\to\sourceFolder -DestinationPath C:\path\to\output.zip -CompressionLevel Optimal
```
{% endcode %}

Decompress a specific file from a ZIP file:

{% code overflow="wrap" %}
```powershell
Expand-Archive -Path C:\path\to\input.zip -DestinationPath C:\path\to\destinationFolder -Include "specificFile.txt"
```
{% endcode %}

Compress files excluding certain files:

{% code overflow="wrap" %}
```powershell
Compress-Archive -Path C:\path\to\sourceFolder\* -DestinationPath C:\path\to\output.zip -Exclude "*.log"
```
{% endcode %}

<mark style="color:yellow;">**makecab**</mark>: Creates cabinet (.cab) files for software distribution (older format).

<mark style="color:yellow;">**extrac32**</mark>: Extracts files from .cab files.

Create a CAB file from a single file:

```powershell
makecab C:\path\to\sourceFile.txt C:\path\to\outputFile.cab
```

Create a CAB file from multiple files using a directive file:

```powershell
makecab /f C:\path\to\directive.ddf
```

Extract files from a CAB file using extrac32:

```powershell
extrac32 C:\path\to\sourceFile.cab C:\path\to\destinationFolder
```

Extract a specific file from a CAB file using extrac32:

```powershell
extrac32 /L C:\path\to\destinationFolder C:\path\to\sourceFile.cab specificFile.txt
```

Display contents of a CAB file without extracting (using extrac32):

```powershell
extrac32 /D C:\path\to\sourceFile.cab
```
