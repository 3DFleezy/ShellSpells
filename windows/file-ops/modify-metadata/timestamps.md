# Timestamps

## <mark style="color:red;">Commands</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="598">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>(Get-Item &#x3C;file>).CreationTime = 'YYYY-MM-DD HH:MM:SS'</code></mark></td><td>Creation</td></tr><tr><td><mark style="color:yellow;"><code>(Get-Item &#x3C;file>).LastAccessTime = 'YYYY-MM-DD HH:MM:SS'</code></mark></td><td>Last Access</td></tr><tr><td><mark style="color:yellow;"><code>(Get-Item &#x3C;file>).LastWriteTime = 'YYYY-MM-DD HH:MM:SS'</code></mark></td><td>Last Modified</td></tr></tbody></table>

## <mark style="color:red;">Timestamp Updates</mark>

### <mark style="color:purple;">Create Time</mark>

The create timestamp is updated anytime a file or directory is created from scratch or a copy is made.

### <mark style="color:purple;">Modify Time</mark>

The modification timestamp is updated anytime a file or directory is changed.

### <mark style="color:purple;">Access Time</mark>

The access timestamp is updated anytime the contents (including metadata) of a file or directory is touched to perform an action.

### <mark style="color:purple;">Entry Modify Time</mark>

The entry modified timestamp refers to the time when the Master File Table (MFT) entry itself was modified.

## <mark style="color:red;">How File Actions Effect Timestamps</mark>

Creating a folder updates the - Modified, Access and Create Times (for the folder)

Creating a file updates the - Modified, Access and Creat Times (for the file)

Creating a file within a folder updates the - Modified and Access Times (for the folder)



Modifying a file updates the - Modified and Access Times (for the file)

Modifying a file updates the - Modified and Access Times (for the folder)



Moving a file into a folder/directory updates the - Modified and Access Times (for the folder/dir)

Moving a file into a folder/directory updates the - Access Time (for the file)



Copying a file into a folder/directory updates the - Access Time (for the directory the file was copied FROM)

Copying a file into a folder/directory updates the - Modified and Access Time (for the directory the file was copied TO)

The difference between a copy and move is that a COPY will create a new file at the destination and results in multiple files and a MOVE will create a new file at the destination and then erases the original file from its location by updating the Master File Table (MFT) to point to the new location.

The default action when a Drag and Drop function is performed within the same partition is a MOVE and when performed on a different partition is a COPY.

## <mark style="color:red;">Enable/Disable Last Access Update Time</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate</mark>

\-> value of 1 means disabled (default in Vista+)

\-> value of 0 means enabled (default in XP and earlier -if the key exists)
