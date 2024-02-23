---
description: Start/Stop and enumerate transcripts.
---

# Transcripts

## <mark style="color:red;">Start/Stop Transcript</mark>

<mark style="color:yellow;">`script surveyTranscript.txt`</mark> \
<mark style="color:yellow;">`exit`</mark>  ends the recording

## <mark style="color:red;">Enumerate Transcripts</mark>

<table data-full-width="true"><thead><tr><th width="384">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>find / -name "*.txt" 2>/dev/null</code></mark></td><td>Searches the entire filesystem for text files, which might include transcript files.</td></tr><tr><td><mark style="color:yellow;"><code>locate *.txt</code></mark></td><td>Uses the <code>locate</code> database to quickly find text files, potentially including transcripts.</td></tr><tr><td><mark style="color:yellow;"><code>grep -ri "Session Start" /file.txt</code></mark></td><td>Recursive case-insensitive search for "Session Start" which can indicate the beginning of a transcript.</td></tr><tr><td><mark style="color:yellow;"><code>ls -ltr /path/to/directory/*.txt</code></mark></td><td>Lists text files in a specified directory in reverse chronological order, helping to identify recently created or modified transcript files.</td></tr></tbody></table>
