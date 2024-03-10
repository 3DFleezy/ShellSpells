# Antivirus

## <mark style="color:red;">Enumerate</mark>

### <mark style="color:purple;">Searching for AV</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>which [AV_command]</code></mark></td><td>Checks if the antivirus executable is installed and accessible in the system's PATH.</td></tr><tr><td><mark style="color:yellow;"><code>ps -ef | grep [AV_process]</code></mark></td><td>Looks for running antivirus processes in the system.</td></tr><tr><td><mark style="color:yellow;"><code>dpkg -l | grep [AV_package]</code></mark></td><td>Checks if the antivirus package is installed on Debian-based systems.</td></tr><tr><td><mark style="color:yellow;"><code>rpm -qa | grep [AV_package]</code></mark></td><td>Checks if the antivirus package is installed on RPM-based systems.</td></tr><tr><td><mark style="color:yellow;"><code>ps aux | grep antivirus</code></mark></td><td>String search for "antivirus" in the process list.</td></tr><tr><td><mark style="color:yellow;"><code>pgrep -f antivirus</code></mark></td><td>String search for "antivirus" in the process command arguments.</td></tr><tr><td><mark style="color:yellow;"><code>/etc/init.d</code></mark></td><td>Look for scripts related to antivirus software.</td></tr><tr><td><mark style="color:yellow;"><code>systemctl list-unit-files --type=service</code></mark></td><td>(Systemd) Check for service unit files related to antivirus software by name or vendor.</td></tr></tbody></table>

### <mark style="color:purple;">File System Exploration</mark>

#### <mark style="color:green;">Locate common antivirus directories:</mark>

Many antiviruses reside in specific directories like\
/usr/local/antivirus\
/opt/antivirus\
vendor-specific locations

#### <mark style="color:green;">Look for signature files:</mark>

Antiviruses often use signature files for malware detection.\
Search for common file extensions like .vdb, .dat, or vendor-specific formats in directories typically used for signatures (e.g., /var/lib/antivirus).

### <mark style="color:purple;">AV Enum Script</mark>

Searches for popular AVs.\
Customize accordingly.

{% hint style="danger" %}
This script has not been tested.
{% endhint %}

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

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo systemctl enable &#x3C;antivirus_service_name></code></mark></td><td>for systemd-based systems</td></tr><tr><td><mark style="color:yellow;"><code>sudo chkconfig &#x3C;antivirus_service_name> on</code></mark></td><td>for SysVinit-based systems</td></tr></tbody></table>

### <mark style="color:purple;">Disable</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo systemctl disable &#x3C;antivirus_service_name></code></mark></td><td>for systemd-based system</td></tr><tr><td><mark style="color:yellow;"><code>sudo chkconfig &#x3C;antivirus_service_name> off</code></mark></td><td>for SysVinit-based systems</td></tr></tbody></table>

### <mark style="color:purple;">Start</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo systemctl start &#x3C;antivirus_service_name></code></mark></td><td>for systemd-based systems</td></tr><tr><td><mark style="color:yellow;"><code>sudo service &#x3C;antivirus_service_name> start</code></mark></td><td>for SysVinit-based systems</td></tr></tbody></table>

### <mark style="color:purple;">Stop</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>sudo systemctl stop &#x3C;antivirus_service_name></code></mark></td><td>for systemd-based systems</td></tr><tr><td><mark style="color:yellow;"><code>sudo service &#x3C;antivirus_service_name> stop</code></mark></td><td>for SysVinit-based systems</td></tr></tbody></table>
