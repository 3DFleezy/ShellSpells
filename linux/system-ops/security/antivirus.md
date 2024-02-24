# Antivirus

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Searching for AV</mark>

| Command                                     | Description                                                                             |
| ------------------------------------------- | --------------------------------------------------------------------------------------- |
| `which [AV_command]`                        | Checks if the antivirus executable is installed and accessible in the system's PATH.    |
| `ps -ef \| grep [AV_process]`               | Looks for running antivirus processes in the system.                                    |
| `dpkg -l \| grep [AV_package]`              | Checks if the antivirus package is installed on Debian-based systems.                   |
| `rpm -qa \| grep [AV_package]`              | Checks if the antivirus package is installed on RPM-based systems.                      |
| `ps aux \| grep antivirus`                  | String search for "antivirus" in the process list.                                      |
| `pgrep -f antivirus`                        | String search for "antivirus" in the process command arguments.                         |
| `/etc/init.d`                               | Look for scripts related to antivirus software.                                         |
| `systemctl list-unit-files --type=service`  | (Systemd) Check for service unit files related to antivirus software by name or vendor. |

### <mark style="color:purple;">File System Exploration</mark>

#### <mark style="color:green;">Locate common antivirus directories:</mark>&#x20;

Many antiviruses reside in specific directories like \
/usr/local/antivirus \
/opt/antivirus \
vendor-specific locations

#### <mark style="color:green;">Look for signature files:</mark>&#x20;

Antiviruses often use signature files for malware detection. \
Search for common file extensions like .vdb, .dat, or vendor-specific formats in directories typically used for signatures (e.g., /var/lib/antivirus).

### <mark style="color:purple;">AV Enum Script</mark>

Searches for popular AVs. \
Customize accordingly.

```bash
#!/bin/bash

# List of common antivirus commands or processes
antivirus_commands=("clamscan" "freshclam" "rkhunter" "chkrootkit" "clamav" "sophos" "avast" "avg" "bitdefender")

# Function to check if a command or process exists
check_existence() {
    if command -v "$1" &>/dev/null || ps -ef | grep -q "$1"; then
        echo "$1 is installed or running."
    else
        echo "$1 is not installed or running."
    fi
}

# Loop through the list of antivirus commands/processes
for antivirus_cmd in "${antivirus_commands[@]}"; do
    check_existence "$antivirus_cmd"
done
```



## <mark style="color:red;">Modify</mark>

### <mark style="color:purple;">Enable</mark>

| Command                                          | Description                |
| ------------------------------------------------ | -------------------------- |
| `sudo systemctl enable <antivirus_service_name>` | for systemd-based systems  |
| `sudo chkconfig <antivirus_service_name> on`     | for SysVinit-based systems |

### <mark style="color:purple;">Disable</mark>

| Command                                           | Description                |
| ------------------------------------------------- | -------------------------- |
| `sudo systemctl disable <antivirus_service_name>` | for systemd-based system   |
| `sudo chkconfig <antivirus_service_name> off`     | for SysVinit-based systems |

### <mark style="color:purple;">Start</mark>

| Command                                         | Description                |
| ----------------------------------------------- | -------------------------- |
| `sudo systemctl start <antivirus_service_name>` | for systemd-based systems  |
| `sudo service <antivirus_service_name> start`   | for SysVinit-based systems |

### <mark style="color:purple;">Stop</mark>

| Command                                        | Description                |
| ---------------------------------------------- | -------------------------- |
| `sudo systemctl stop <antivirus_service_name>` | for systemd-based systems  |
| `sudo service <antivirus_service_name> stop`   | for SysVinit-based systems |
