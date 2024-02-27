# Forensically Relevant Keys

## <mark style="color:red;">All</mark>

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList</mark>

Stores user profiles information, including SID, profile path, and last login time.

<mark style="color:blue;">HKEY\_USERS.DEFAULT\Software\Microsoft\Windows\CurrentVersion\Explorer</mark>

Contains settings and information for the default user profile, including RunMRU (most recently used commands).

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU</mark>

Keeps track of files recently opened or saved, providing a history of file activity.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters</mark>

Holds network configuration details, such as DHCP and IP address information.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation</mark>

Contains the system's time zone settings, important for timestamp analysis.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall</mark>

Lists installed software, including installation dates and versions.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs</mark>

Tracks documents recently accessed by the user.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR</mark>

Records history of USB storage devices connected to the computer.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings</mark>

Stores Internet settings, including proxy configurations.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon</mark>

Provides details on Windows logon settings and last logged-on user.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Run</mark>

Contains programs set to run at user login, indicating user preferences or potential malware.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run</mark>

Lists programs set to run at system startup, important for identifying startup items and malware.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce</mark>

Holds commands that run once at the next user login, used for setups and potentially malicious activities.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce</mark>

Contains commands that run once at the next system startup, relevant for installations and malware analysis.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters</mark>

Provides information about the Prefetch feature, which logs files used during system startup and application launch.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders</mark>

Contains paths to various important system folders, useful for understanding system configuration and user behavior.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog</mark>

Stores configuration for event logs, crucial for understanding system events and changes.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows</mark>

Contains settings related to Windows GUI and system parameters, including AppInit\_DLLs which may indicate malware presence.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Office</mark>

Holds Microsoft Office settings, including MRUs and user preferences, useful in user activity analysis.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects</mark>

Lists Browser Helper Objects (BHOs) for Internet Explorer, which can indicate installed toolbars or potential browser-based malware.

<mark style="color:blue;">HKLM\Software\Microsoft\Windows NT\CurrentVersion\Schedule\Taskcache\Tasks</mark>

<mark style="color:blue;">HKLM\SYSTEM\CurrentControlSet\SERVICES\</mark></mark>

<mark style="color:blue;">HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR</mark>

<mark style="color:blue;">HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles\</mark></mark>

<mark style="color:blue;">HKU\<SID>\Software\Microsoft\Internet Explorer\TypedUrls</mark>

## <mark style="color:red;">Persistence Keys</mark>

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Run</mark>

Programs in this key run automatically when the current user logs in.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run</mark>

Programs listed here run automatically for all users at system startup.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce</mark>

Commands or programs here run once at the next user login.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce</mark>

Commands or programs in this key run once at the next system startup.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run</mark>

Programs listed here are executed at system startup.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run</mark>

Programs listed here are executed at user login.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Winlogon</mark>

Entries such as 'Userinit' and 'Shell' can be modified to run custom scripts or applications during the logon process.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\Load</mark>

Specifies programs to load at user login.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows\Load</mark>

Specifies programs to load at system startup.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\Run</mark>

Specifies additional programs to run at user login.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows\Run</mark>

Specifies additional programs to run at system startup.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellExecuteHooks</mark>

Hooks that can be used to execute code when certain actions occur.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services</mark>

Services listed here are started by the Service Control Manager. Malware can create or modify existing services.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders</mark>

Customization of user shell folders can be used for persistence.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders</mark>

Customization of shell folders at a system-wide level.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components</mark>

Components listed here are executed when a user logs in for the first time and when creating new user accounts.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run</mark>

On 64-bit systems, this key is used to run 32-bit applications at system startup.

<mark style="color:blue;">HKEY\_LOCAL\_MACHINE\SOFTWARE\Classes\*\ShellEx\ContextMenuHandlers</mark>

Context menu handlers can be used to execute code when certain file types are right-clicked.

<mark style="color:blue;">HKEY\_CURRENT\_USER\Software\Classes\*\ShellEx\ContextMenuHandlers</mark>

Context menu handlers for specific file types under the current user profile.

<mark style="color:blue;">HKLM\Software\Microsoft\Windows\CurrentVersion\Run</mark>

<mark style="color:blue;">HKU\<SID>\Software\Microsoft\Windows\CurrentVersion\Run</mark>

<mark style="color:blue;">HKLM\BCD00000000</mark>

<mark style="color:blue;">HKLM\SAM\SAMs</mark>

## <mark style="color:red;">Notes</mark>

### <mark style="color:purple;">Root Keys:</mark>

HKLM (local machine)&#x20;

HKCU (current user)&#x20;

HKCR (classes root)&#x20;

HKU (users)&#x20;

HKCC (current configuration).

### <mark style="color:purple;">Value Types:</mark>

REG\_SZ (string)&#x20;

REG\_DWORD (32-bit integer)&#x20;

REG\_QWORD (64-bit integer)&#x20;

REG\_BINARY (binary data)&#x20;

REG\_EXPAND\_SZ (expandable string)
