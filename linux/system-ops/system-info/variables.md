# Variables

## <mark style="color:red;">Enumerate</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="178">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>env</code></td><td>Displays environment variables.</td></tr><tr><td><code>printenv</code></td><td>Similar to env, also lists environment variables.</td></tr><tr><td><code>set</code></td><td>Lists shell variables and functions (bash-specific).</td></tr><tr><td><code>declare -p</code></td><td>Lists shell variables with their attributes (bash-specific).</td></tr><tr><td><code>export</code></td><td>Displays exported variables (visible to child processes).</td></tr></tbody></table>



## <mark style="color:red;">Modify</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><code>export VAR_NAME=VALUE</code></td><td>Sets an environment variable for the current shell and child processes.</td></tr><tr><td><code>VAR_NAME=VALUE</code></td><td>Sets a variable for the current shell only (not inherited by child processes).</td></tr></tbody></table>

### <mark style="color:purple;">Sourcing files</mark>

Use `source filename` or `. filename` to import variables from a file into the current shell environment.



## <mark style="color:red;">Environment Variables</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="197">Variable</th><th>Description</th></tr></thead><tbody><tr><td>PATH</td><td>Contains a colon-separated list of directories where executable files are located.</td></tr><tr><td>HOME</td><td>Stores the absolute path to the user's home directory.</td></tr><tr><td>USER (or LOGNAME)</td><td>Contains the username of the currently logged-in user.</td></tr><tr><td>SHELL</td><td>Specifies the default shell for the user.</td></tr><tr><td>PS1</td><td>Defines the primary shell prompt.</td></tr><tr><td>PS2</td><td>Defines the secondary prompt used when entering multi-line commands.</td></tr><tr><td>PS3</td><td>Specifies the prompt for the select loop in shell scripts.</td></tr><tr><td>PS4</td><td>Specifies the prompt for debugging shell scripts with the -x option.</td></tr><tr><td>PWD</td><td>Holds the current working directory.</td></tr><tr><td>OLDPWD</td><td>Contains the previous working directory.</td></tr><tr><td>TZ</td><td>Specifies the system's timezone.</td></tr><tr><td>IFS</td><td>Defines the Internal Field Separator, which is used to separate words in shell commands.</td></tr><tr><td>TERM</td><td>Specifies the type of terminal or terminal emulator being used.</td></tr><tr><td>EDITOR</td><td>Sets the default text editor used by some command-line utilities.</td></tr><tr><td>VISUAL</td><td>Specifies the default visual (graphical) editor used by some utilities.</td></tr><tr><td>LANG</td><td>Specifies the default system language and localization settings.</td></tr><tr><td>LC_*</td><td>A family of variables used for localization and character encoding settings.</td></tr><tr><td>MAIL</td><td>Points to the location of the user's mailbox or mail spool file.</td></tr><tr><td>MAILCHECK</td><td>Specifies how often to check for new mail.</td></tr><tr><td>MAILPATH</td><td>Contains a list of files to check for new mail.</td></tr><tr><td>LD_LIBRARY_PATH</td><td>Lists directories where the dynamic linker/loader searches for shared libraries.</td></tr><tr><td>LD_PRELOAD</td><td>Specifies shared libraries to be loaded before all others when a program is run.</td></tr><tr><td>MANPATH</td><td>Defines the path to the directory containing manual pages (man pages).</td></tr></tbody></table>



## <mark style="color:red;">File Locations</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th width="291">Type</th><th>Description</th></tr></thead><tbody><tr><td>Environment Variables</td><td>Often set in startup scripts like .bashrc, .bash_profile, or system-wide configuration files.</td></tr><tr><td>User Environment Variables</td><td>Typically set in the user's shell initialization files (e.g., .bashrc, .bash_profile, .profile) or by using the export command in the shell.</td></tr><tr><td>System Environment Variables</td><td>System-wide environment variables can be set in system-wide initialization scripts, such as /etc/environment on some Linux distributions.</td></tr><tr><td>Global System Variables</td><td>Some system-level variables are stored in system configuration files or directories. These can include variables related to network configuration, system parameters, and system behavior. These variables are often stored in files located in /etc or other system directories.</td></tr><tr><td>User-Specific Configuration Files</td><td>User-specific configuration files may store variables related to a specific user's environment and preferences. For example, the ~/.bashrc or ~/.bash_profile files can contain user-specific variables and configurations.</td></tr></tbody></table>
