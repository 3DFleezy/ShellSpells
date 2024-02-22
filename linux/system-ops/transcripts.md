---
description: Start/Stop and enumerate transcripts.
---

# Transcripts

## Start/Stop Transcript

<mark style="color:red;">`script surveyTranscript.txt`</mark> \
<mark style="color:red;">`exit`</mark>  ends the recording

## Enumerate Transcripts

<table data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:red;"><code>find / -name "*.txt" 2>/dev/null</code></mark></td><td>Searches the entire filesystem for text files, which might include transcript files.</td></tr><tr><td><mark style="color:red;"><code>locate *.txt</code></mark></td><td>Uses the <code>locate</code> database to quickly find text files, potentially including transcripts.</td></tr><tr><td><mark style="color:red;"><code>grep -ri "Session Start" /path/to/directory</code></mark></td><td>Recursive case-insensitive search for "Session Start" which can indicate the beginning of a transcript.</td></tr><tr><td><mark style="color:red;"><code>ls -ltr /path/to/directory/*.txt</code></mark></td><td>Lists text files in a specified directory in reverse chronological order, helping to identify recently created or modified transcript files.</td></tr></tbody></table>
