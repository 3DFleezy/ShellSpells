# Remote Command Execution

## Remote Command Syntax

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>PsExec \\&#x3C;RemoteComputerName> cmd.exe /c &#x3C;command></code></mark></td><td>PsExec (Sysinternals) allows you to execute processes remotely.</td></tr><tr><td><mark style="color:yellow;"><code>psexec \\RemoteComputerName ipconfig</code></mark></td><td>Example</td></tr><tr><td><mark style="color:yellow;"><code>psexec \\RemoteComputerName -u Username -p Password cmd.exe /c CommandToRun</code></mark></td><td>PsExec with explicit credentials.</td></tr><tr><td><mark style="color:yellow;"><code>Invoke-Command -ComputerName RemoteComputerName -ScriptBlock { CommandToRun }</code></mark></td><td>PowerShell cmdlet</td></tr><tr><td><mark style="color:yellow;"><code>Invoke-Command -ComputerName RemoteComputerName -ScriptBlock { Get-Process }</code></mark></td><td>Example</td></tr><tr><td><mark style="color:yellow;"><code>Invoke-Expression</code></mark></td><td>Not intended for remote execution, but can with the necessary permissions.</td></tr><tr><td><mark style="color:yellow;"><code>mstsc /v:RemoteComputerName</code></mark></td><td>The Remote Desktop Command (<code>mstsc</code>) (GUI App, but does command open GUI?)</td></tr><tr><td><mark style="color:yellow;"><code>WinRS -r:RemoteComputerName &#x3C;command></code></mark></td><td>Windows Remote Shell (WinRS)</td></tr><tr><td><mark style="color:yellow;"><code>winrs -r:http://RemoteComputerName &#x3C;command></code></mark></td><td>Example</td></tr><tr><td><mark style="color:yellow;"><code>ssh username@RemoteComputerName CommandToRun</code></mark></td><td>SSH</td></tr><tr><td><mark style="color:yellow;"><code>Enter-PSSession -ComputerName RemoteComputerName</code></mark></td><td>Start interactive session with a remote computer.</td></tr><tr><td><mark style="color:yellow;"><code>Invoke-Expression -Command "Enter-PSSession -ComputerName RemoteComputerName"</code></mark></td><td>Example</td></tr><tr><td><mark style="color:yellow;"><code>wmic /node:"RemoteComputerName" process call create "&#x3C;command>"</code></mark></td><td>WMIC.</td></tr><tr><td><mark style="color:yellow;"><code>wmic /node:"RemoteComputerName" process list</code></mark></td><td>Example</td></tr><tr><td><mark style="color:yellow;"><code>wmic /node:"RemoteComputerName" os get caption</code></mark></td><td>Another Example</td></tr><tr><td><mark style="color:yellow;"><code>sc \\RemoteComputerName start ServiceName</code></mark></td><td>Remote service start.</td></tr></tbody></table>

Example:

```powershell
Get-Hotfix -ComputerName win10 -Credential administrator (prompt for PW)
```

```powershell
$c = Get-Credential -UserName "win10\user" -Message:"Enter password:"
```

```powershell
Get-Hotfix -ComputerName win10 -Credential $c
```

```powershell
Get-Hotfix -computername win10 -credential $c | where {$_.Description -match "Security"}
```

## PS Sessions

1. Establish Creds

```powershell
$cred = Get-Credential -UserName "win7\User"  -Message:"Enter password:"
```

2. Issue Remote Command

```powershell
Get-Hotfix -ComputerName win7 -Credential $cred
```

3. Establish PSSession

```powershell
$session 7 = New-PSSession -computername win7 -Credentail $cred
```

4A) Enter Commands to PSSession

```powershell
Invoke-Command -session $session7 {get-process}
```

4B) Interactively Control

```powershell
` Enter-PSSession -session7 $session7
```

```powershell
Get-Process
```

```powershell
Get-Service | Where {$_.Status -like "Running"
```

```powershell
Exit-PSSession
```

## Commands with Remote Options

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>reg /s "C:\Path\To\Your\RegistryFile.reg"</code></mark></td><td><mark style="color:yellow;"><code>/s</code></mark>parameter to import registry changes remotely by specifying the remote computer's registry path.</td></tr><tr><td><mark style="color:yellow;"><code>reg import \\RemoteComputerName\Share\RegistryFile.reg</code></mark></td><td>Remote registry import</td></tr><tr><td><mark style="color:yellow;"><code>sc \\RemoteComputerName stop "ServiceName"</code></mark></td><td>Allows you to manage and configure Windows services on remote computers.</td></tr><tr><td><mark style="color:yellow;"><code>sc \\RemoteComputerName query</code></mark></td><td>Query services on remote computers.</td></tr><tr><td><mark style="color:yellow;"><code>netsh -r RemoteComputerName interface show interface</code></mark></td><td>You can use <mark style="color:yellow;"><code>netsh</code></mark>to configure network settings on remote Windows systems if you have appropriate permissions.</td></tr><tr><td><mark style="color:yellow;"><code>tasklist /s RemoteComputerName</code></mark></td><td>The <mark style="color:yellow;"><code>tasklist</code></mark>command with the <mark style="color:yellow;"><code>/s</code></mark>parameter allows you to list running processes on a remote computer.</td></tr><tr><td><mark style="color:yellow;"><code>query user /server</code></mark></td><td>Displays information about user sessions on a remote server.</td></tr><tr><td><mark style="color:yellow;"><code>query process /server</code></mark></td><td>Lists processes running on a remote server.</td></tr><tr><td><mark style="color:yellow;"><code>gpupdate /target:computer /force</code></mark></td><td>Forces a remote update of Group Policy settings on a computer.</td></tr><tr><td><mark style="color:yellow;"><code>wmic /node /output</code></mark></td><td>Allows you to run a specific command on multiple remote computers and save the output to a file.</td></tr><tr><td><mark style="color:yellow;"><code>taskkill /s</code></mark></td><td>Terminates processes on a remote computer specified by its name or IP.</td></tr><tr><td><mark style="color:yellow;"><code>ssh username@RemoteComputerName "ls"</code></mark></td><td>Run remote command</td></tr></tbody></table>

Allows you to schedule tasks remotely on other Windows computers:

{% code overflow="wrap" %}
```powershell
schtasks /create /s RemoteComputerName /tn "MyTask" /tr "C:\MyScript.bat" /sc daily /st 08:00
```
{% endcode %}
