# Shares

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Samba (Windows Shares)</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="361">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>smbclient -L &#x3C;server_name></code></mark></td><td>Lists shares available on a specific Windows server.</td></tr><tr><td><mark style="color:yellow;"><code>smbclient -L //&#x3C;hostname></code></mark></td><td>List available SMB/CIFS shares on a remote Samba server (replace <mark style="color:yellow;"><code>&#x3C;hostname></code></mark> with the server's hostname or IP address).</td></tr><tr><td><mark style="color:yellow;"><code>netstat -tuln</code></mark></td><td>Display listening network services and ports. Look for services like NFS (port 2049) or Samba (ports 137-139 and 445).</td></tr><tr><td><mark style="color:yellow;"><code>nmap -p 139,445 &#x3C;network_range></code></mark></td><td>Scans a network range for active Samba servers (requires nmap installation).</td></tr><tr><td><mark style="color:yellow;"><code>smbmap</code></mark></td><td>Lists shares from multiple servers based on /etc/samba/smb.conf configuration.</td></tr></tbody></table>

### <mark style="color:purple;">NFS (Network File System)</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="358">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>mount</code></mark></td><td>List currently mounted filesystems, including network shares like NFS and CIFS/SMB.</td></tr><tr><td><mark style="color:yellow;"><code>showmount -e</code></mark></td><td>Lists NFS exports (shared directories) from accessible NFS servers.</td></tr><tr><td><mark style="color:yellow;"><code>showmount -e &#x3C;hostname></code></mark></td><td>List NFS shares available on a remote NFS server (replace <mark style="color:yellow;"><code>&#x3C;hostname></code></mark> with the server's hostname or IP address).</td></tr><tr><td><mark style="color:yellow;"><code>rpcinfo -p mountd &#x3C;server_name></code></mark></td><td>Checks NFS availability on a specific server.</td></tr><tr><td><mark style="color:yellow;"><code>nfsstat -s</code></mark></td><td>Shows mounted NFS shares on the local system. (client perspective)</td></tr><tr><td><mark style="color:yellow;"><code>nfsstat -m</code></mark></td><td>Show NFS-mounted filesystems on the local system.</td></tr><tr><td><mark style="color:yellow;"><code>findmnt -t nfs -t cifs</code></mark></td><td>List mounted NFS and CIFS filesystems.</td></tr></tbody></table>

### <mark style="color:purple;">WebDAV Shares</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="344">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>curl -I &#x3C;URL></code></mark></td><td>Checks the headers of a URL to see if it's a WebDAV server.</td></tr><tr><td><mark style="color:yellow;"><code>davfs2</code></mark></td><td>Mounts WebDAV shares as local directories (tool) (requires installation).</td></tr></tbody></table>

## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">NFS (Network File System)</mark>

#### <mark style="color:green;">Create an NFS Export</mark>

Modify the /etc/exports file to specify which directories to export and the access permissions. Example: <mark style="color:yellow;">`sudo nano /etc/exports`</mark>\
Add an entry like: <mark style="color:orange;">/shared\_directory 192.168.1.0/24(rw,sync,no\_root\_squash)</mark>

#### <mark style="color:green;">Restart NFS Server</mark>

Reload or restart the NFS server to apply changes.\
Example: <mark style="color:yellow;">`sudo systemctl restart nfs-server`</mark>

#### <mark style="color:green;">Mount an NFS Share</mark>

Use the mount command to connect to an NFS share.\
Example: <mark style="color:yellow;">`sudo mount -t nfs <server_ip>:/shared_directory /mnt/mount_point`</mark>

### <mark style="color:purple;">Samba (SMB/CIFS)</mark>

#### <mark style="color:green;">Install Samba</mark>

Ensure Samba is installed on your system.\
Example (on Debian/Ubuntu): <mark style="color:yellow;">`sudo apt-get install samba`</mark>

<mark style="color:green;">Create a Samba Share</mark>

Create a share on a Samba server (requires administrative privileges):\
<mark style="color:yellow;">`smbcontrol server <server_name> share add <share_name> <path>`</mark>

Export a directory on your system as an NFS share (requires administrative privileges):\
<mark style="color:yellow;">`export <path>`</mark>

AND/OR

Modify the Samba configuration file (smb.conf) to define your shares.\
<mark style="color:yellow;">`sudo nano /etc/samba/smb.conf`</mark>\
Add an entry like:

```bash
[MyShare]
path = /shared_directory
read only = no
```

#### <mark style="color:green;">Set Samba Passwords</mark>

Create a Samba user and set the password.\
Example: <mark style="color:yellow;">`sudo smbpasswd -a <username>`</mark>

#### <mark style="color:green;">Restart Samba</mark>

Restart the Samba service to apply changes.\
Example: <mark style="color:yellow;">`sudo systemctl restart smbd`</mark>

#### <mark style="color:green;">Connect to a Samba Share</mark>

Use the <mark style="color:yellow;">`smbclient`</mark> command to connect to a Samba share interactively.\
<mark style="color:yellow;">`smbclient //<server_ip>/MyShare -U <username>`</mark>

Connect to a share for editing files. Requires appropriate permissions:\
<mark style="color:yellow;">`smbclient -U <server_name>/<share_name>`</mark>

<mark style="color:green;">Mount a Samba Share (CIFS)</mark>

Use the <mark style="color:yellow;">`mount`</mark> command to mount a Samba share to a local directory.\
Example: <mark style="color:yellow;">`sudo mount -t cifs -o username=<user>,password=<password> //<server_ip>/MyShare /mnt/mount_point`</mark>

Mount a share temporarily:\
<mark style="color:yellow;">`smbmount //<server_name>/<share_name> /mnt/sharepoint`</mark>

Mounts a share permanently using credentials:\
<mark style="color:yellow;">`mount.cifs //<server_name>/<share_name> /mnt/sharepoint -o username=<user>,password=<password>`</mark>

### <mark style="color:purple;">WebDAV</mark>

#### <mark style="color:green;">Modifying</mark>

Mount a WebDAV share as a local directory for editing files (requires the davfs2 package):\
`davfs2 /url/to/webdav /mnt/sharepoint`

#### <mark style="color:green;">Creating</mark>

WebDAV servers usually have web interfaces for creating shares. Consult the server's documentation.

#### <mark style="color:green;">Connecting</mark>

Same as modifying.
