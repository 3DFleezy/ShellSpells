# Enumerate

## <mark style="color:red;">Enum Script</mark>

This script checks existence all potential startup script locations. \
It prints file path if it exists. \
It checks file permissions to see if current user can edit. \
If so, it colors it red.

{% hint style="danger" %}
This script is AI generated, NOT TESTED, and probably does not work.&#x20;

I only included it because it has potentially useful sections that you can build from.
{% endhint %}

<pre class="language-bash"><code class="lang-bash">#!/bin/bash



<strong># Define an array of potential autostart script locations
</strong>autostart_locations=(
    "/etc/rc.local"
    "/etc/rc.d/rc.local"
    "/etc/init.d"
    "/etc/systemd/system"
    "/etc/systemd/system/multi-user.target.wants/"
    "/etc/systemd/user"
    "/usr/lib/systemd/system"
    "/lib/systemd/system"
    "/etc/xdg/autostart"
    "/home/$USER/.config/autostart"
)

<strong># Function to check file/directory and print details
</strong>check_and_print() {
    local path="$1"
    if [ -e "$path" ]; then
        # Check if the current user has write permission
        if [ -w "$path" ]; then
            # Print path in red with permissions
            echo -e "\033[31m$(ls -ld "$path")\033[0m"
        else
            # Print path with permissions
            echo "$(ls -ld "$path")"
        fi
    fi
}

# Iterate over locations and check each
for location in "${autostart_locations[@]}"; do
    if [ -d "$location" ]; then
        # If it's a directory, check each file in it
        for file in "$location"/*; do
            check_and_print "$file"
        done
    else
        # If it's a file, just check the file
        check_and_print "$location"
    fi
done
</code></pre>

## <mark style="color:red;">System-wide Startup Files</mark>

| File/Directory      | Description                                                                                                    |
| ------------------- | -------------------------------------------------------------------------------------------------------------- |
| /etc/inittab        | (SysV init) Controls the boot process and launches initial scripts based on run levels.                        |
| /etc/systemd/system | (systemd) Contains systemd unit files defining services and processes to start at boot.                        |
| /etc/rc.local       | (SysV init) Allows adding custom scripts to be executed at boot (may not be present or active on all systems). |
| /etc/default/\*     | Holds configuration files for various system services (e.g., /etc/default/syslog).                             |
| /etc/profile        | System-wide shell configuration file, often sourced by other files.                                            |
| /etc/bashrc         | System-wide Bash shell configuration file.                                                                     |
| /etc/zsh/zshrc      | System-wide Zsh shell configuration file. (Other shells might have different files)                            |
| /etc/profile.d/     | Files placed here are sourced for all users' login shells (similar to .profile).                               |
| /etc/bashrc.d/      | Files here are specifically for bash login shells.                                                             |

## <mark style="color:red;">User-specific Startup Files</mark>

<mark style="color:orange;">**\~/.profile**</mark>\
User-specific shell configuration file, sourced at login. \


<mark style="color:orange;">**\~/.xsession**</mark> or <mark style="color:orange;">**\~/.xinitrc**</mark>\
Configuration for graphical login sessions (depending on the desktop environment).

## <mark style="color:red;">Bourne-Again Shell (bash)</mark>

<mark style="color:orange;">**\~/.bash\_profile**</mark>, <mark style="color:orange;">**\~/.bash\_login**</mark>, or <mark style="color:orange;">**\~/.profile**</mark> (in order of preference) \
These files are read and executed when a bash login shell is started. \
<mark style="color:orange;">**\~/.bash\_profile**</mark> is the most commonly used file for login sessions.

<mark style="color:orange;">**\~/.bashrc**</mark>\
While not a login script per se, it's often sourced by the login scripts or interactive shells to configure the shell session. \
It's used mainly for interactive shell behavior, aliases, and functions.

## <mark style="color:red;">Z Shell (zsh)</mark>

<mark style="color:orange;">**\~/.zprofile**</mark> \
Similar to \~/.bash\_profile for bash, this file is executed for login shells.

<mark style="color:orange;">**\~/.zshrc**</mark> \
Executed for interactive shell sessions. \
It's common to place most shell customizations here.

## <mark style="color:red;">C Shell (csh) or TENEX C Shell (tcsh)</mark>

<mark style="color:orange;">**\~/.login**</mark>\
Executed at the beginning of a csh or tcsh login shell session.

<mark style="color:orange;">**\~/.cshrc (csh)**</mark> or <mark style="color:orange;">**\~/.tcshrc (tcsh)**</mark>\
Read and executed when an interactive shell session starts. \
It's used for setting up the shell environment.

## <mark style="color:red;">Korn Shell (ksh)</mark>

<mark style="color:orange;">**\~/.profile**</mark> \
Executed for login shells. \
Ksh shares this file with Bourne Shell (sh) and bash when running as sh.

## <mark style="color:red;">SysV Init</mark>

<mark style="color:orange;">**/etc/inittab**</mark> \
Configuration file specifying the default runlevel and how the system initializes processes. Used by older Unix systems.

<mark style="color:orange;">**/etc/rc.d/**</mark> or <mark style="color:orange;">**/etc/init.d/**</mark> \
Directory containing startup scripts (init scripts) for various services and daemons.

<mark style="color:orange;">**/etc/rc.local**</mark> \
A script that is executed at the end of the SysV init process. \
You can add custom startup commands here.

<mark style="color:orange;">**/etc/rc?.d**</mark> \
Directories for runlevels 0-6, S (e.g., /etc/rc3.d). \
Scripts in these directories are symbolic links to scripts in /etc/init.d and are executed at different runlevel

## <mark style="color:red;">Systemd</mark>

<mark style="color:orange;">**/etc/systemd/system/**</mark> \
Directory containing systemd service unit files.

<mark style="color:orange;">**/lib/systemd/system**</mark> and <mark style="color:orange;">**/usr/lib/systemd/system**</mark> \
Directories where packaged unit files are typically located. \
These should not be modified directly; instead, override files should be placed in /etc/systemd/system.

<mark style="color:orange;">**/lib/systemd/system**</mark> and <mark style="color:orange;">**/usr/lib/systemd/system**</mark> \
Directories where packaged unit files are typically located. \
These should not be modified directly; instead, override files should be placed in /etc/systemd/system.

<mark style="color:orange;">**/etc/systemd/system/\***</mark> \
Directory containing systemd unit files for various services, including boot services.

<mark style="color:orange;">**/etc/systemd/system/default.target**</mark> \
Symbolic link specifying the default target (runlevel) that systemd boots into. \
Equivalent to runlevels in SysV.

<mark style="color:orange;">**/etc/systemd/system/multi-user.target**</mark> \
Unit file defining the multi-user target (runlevel equivalent). \
Units with "Requires=multi-user.target" Services dependent on the multi-user target, likely executed during boot.

<mark style="color:orange;">**/etc/systemd/system.conf**</mark> \
Main configuration file for systemd.

<mark style="color:orange;">**\~/.config/systemd/user/**</mark> \
User-specific systemd unit files for services started with the user's session.

<mark style="color:orange;">**/etc/systemd/system/multi-user.target.wants/**</mark>, <mark style="color:orange;">**/etc/systemd/system/graphical.target.wants/**</mark>, etc. \
Directories containing symlinks to unit files for services that should be started automatically under specific targets.

## <mark style="color:red;">Upstart</mark>

<mark style="color:orange;">**/etc/init/**</mark>\
Directory containing Upstart job configuration files. \
Jobs define how services are started, stopped, and managed (not to be confused with /etc/init.d used by SysV).

<mark style="color:orange;">**/etc/init.d/**</mark>\
Directory containing SysV-style init scripts. For compatibility with SysV init scripts, Upstart systems may also include this directory. While Upstart itself does not use these scripts directly, it provides backward compatibility allowing administrators to manage services using traditional SysV init scripts. \
Upstart intercepts calls to the service and /etc/init.d/ scripts and translates them into appropriate Upstart events when possible.

<mark style="color:orange;">**/etc/init/rc-sysinit.conf**</mark>\
Upstart configuration file responsible for initializing the system, similar to SysV's init scripts.

<mark style="color:orange;">**/etc/init/rc.conf**</mark>\
Upstart configuration file specifying the default runlevel.

<mark style="color:orange;">**/etc/init/tty.conf\***</mark>\
Upstart job configuration files for handling virtual terminals (ttys).

<mark style="color:orange;">**\~/.init/**</mark>\
User-specific Upstart job configuration directory for custom jobs.
