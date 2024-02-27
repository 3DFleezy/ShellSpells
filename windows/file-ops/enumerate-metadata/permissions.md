# Permissions

## Commands

<table data-header-hidden data-full-width="true"><thead><tr><th width="652">Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>icacls &#x3C;file></code></mark></td><td>For file or directory</td></tr><tr><td><mark style="color:yellow;"><code>Get-Acl &#x3C;Path\FileName></code></mark></td><td>Detailed permissions</td></tr><tr><td><mark style="color:yellow;"><code>Get-Acl &#x3C;Path\FileName> | Select-Object -ExpandProperty Access</code></mark></td><td>Detailed access rights for each trustee of the file</td></tr></tbody></table>

## Permissions Explained

<mark style="color:orange;">(OI)</mark>: Object Inherit - This ACE (Access Control Entry) is inherited by files.

<mark style="color:orange;">(CI)</mark>: Container Inherit - This ACE is inherited by directories.

<mark style="color:orange;">(IO)</mark>: Inherit Only - This ACE does not apply to the current file/directory.

<mark style="color:orange;">(NP)</mark>: No Propagate - This ACE is not propagated to child objects.

<mark style="color:orange;">(I)</mark>: Inherited - The ACE was inherited from the parent container's ACL.

<mark style="color:orange;">F</mark>: Full Control - The trustee can read, write, execute, change permissions, and take ownership of the file or directory.

<mark style="color:orange;">M</mark>: Modify - The trustee can read, write, execute, and delete the file or directory.

<mark style="color:orange;">RX</mark>: Read & Execute - The trustee can read and execute the file or directory.

<mark style="color:orange;">R</mark>: Read - The trustee can read the contents of the file or directory but cannot make any changes.

<mark style="color:orange;">W</mark>: Write - The trustee can write to the file or directory but cannot read its contents.
