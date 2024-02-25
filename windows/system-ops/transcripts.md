# Transcripts

## Start/Stop

| Command                                              | Description      |
| ---------------------------------------------------- | ---------------- |
| `Start-Transcript -Path "C:\path\to\transcript.txt"` | Start transcript |
| `Stop-Transcript`                                    | Stop Transcript  |

## Enumerate Transcripts

Default Transcripts Location: <mark style="color:orange;">%UserProfile%\Documents\PowerShell\_transcript\<HostName></mark>_<mark style="color:orange;">YYYYMMDDHHMMSS</mark>_<mark style="color:orange;">\<TranscriptFileName>.txt</mark>

{% code overflow="wrap" %}
```powershell
Get-ChildItem -Path "$env:USERPROFILE\Documents\PowerShell_transcript\" -Filter "*.txt"
```
{% endcode %}

```powershell
dir "%USERPROFILE%\Documents\PowerShell_transcript\*.txt" /s /b
```
