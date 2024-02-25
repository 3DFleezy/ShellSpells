# Copy

| Command | Description |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| <mark style="color:yellow;">`cp [file] /dir`</mark>                   | Copy to /dir.                                                                                                 |
| <mark style="color:yellow;">`cp [file] new_name`</mark>               | Rename                                                                                                        |
| <mark style="color:yellow;">`cp -r source_dir /dir`</mark>            | Recursive                                                                                                     |
| <mark style="color:yellow;">`cp -p [file] /dir`</mark>                | Preserve its mode, ownership, and timestamps.                                                                 |
| <mark style="color:yellow;">`cp -i [file] /dir`</mark>                | Interactively, prompting before overwrite.                                                                    |
| <mark style="color:yellow;">`cp -v [file] /dir`</mark>                | Verbose output, showing the file names as they are copied.                                                    |
| <mark style="color:yellow;">`cp -n [file] /dir`</mark>                | No Clobber. Won't overwriting any existing file in the target location.                                       |
| <mark style="color:yellow;">`rsync -av [file] /dir`</mark>            | Archive mode to preserve permissions and verbose output.                                                      |
| <mark style="color:yellow;">`rsync -av --progress [file] /dir`</mark> | Displays progress.                                                                                            |
| <mark style="color:yellow;">`rsync -av --delete /src_dir /dir`</mark> | Sync contents of `/src_dir` to `/dir`, deleting files in `/dir` that are not in `/src_dir`.                   |
| <mark style="color:yellow;">`rsync -av --dry-run [file] /dir`</mark>  | Simulate the file copy operation without actually copying any files. Useful for checking what will be copied. |



Copy over SSH to a remote system, compressing file data during the transfer:

```bash
rsync -avz -e ssh [file] user@remote_host:/dir
```
