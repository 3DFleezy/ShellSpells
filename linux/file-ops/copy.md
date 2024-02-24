# Copy

| Command                            | Description                                                                                                   |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `cp [file] /dir`                   | Copy to /dir.                                                                                                 |
| `cp [file] new_name`               | Rename                                                                                                        |
| `cp -r source_dir /dir`            | Recursive                                                                                                     |
| `cp -p [file] /dir`                | Preserve its mode, ownership, and timestamps.                                                                 |
| `cp -i [file] /dir`                | Interactively, prompting before overwrite.                                                                    |
| `cp -v [file] /dir`                | Verbose output, showing the file names as they are copied.                                                    |
| `cp -n [file] /dir`                | No Clobber. Won't overwriting any existing file in the target location.                                       |
| `rsync -av [file] /dir`            | Archive mode to preserve permissions and verbose output.                                                      |
| `rsync -av --progress [file] /dir` | Displays progress.                                                                                            |
| `rsync -av --delete /src_dir /dir` | Sync contents of `/src_dir` to `/dir`, deleting files in `/dir` that are not in `/src_dir`.                   |
| `rsync -av --dry-run [file] /dir`  | Simulate the file copy operation without actually copying any files. Useful for checking what will be copied. |



Copy over SSH to a remote system, compressing file data during the transfer:

```bash
rsync -avz -e ssh [file] user@remote_host:/dir
```
