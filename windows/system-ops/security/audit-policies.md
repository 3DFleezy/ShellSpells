# Audit Policies

## <mark style="color:red;">Enumerate</mark>

<table data-header-hidden data-full-width="true"><thead><tr><th>Command</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:yellow;"><code>auditpol /get /category:*</code></mark></td><td>Current audit policy settings for all categories.</td></tr><tr><td><mark style="color:yellow;"><code>auditpol /get /User:UserName / Category:*</code></mark></td><td>Current audit policy settings for user, all audit categories.</td></tr><tr><td><mark style="color:yellow;"><code>auditpol /List /User /V</code></mark></td><td>All user-level audit policy settings.</td></tr><tr><td><mark style="color:yellow;"><code>auditpol (auditpol /get /category:*)</code></mark></td><td>Check policies &#x3C;auditusr on xp/2003></td></tr><tr><td><mark style="color:yellow;"><code>Get-AuditPolicy</code></mark></td><td>Gets the audit policy for one or more audit subcategories.</td></tr><tr><td><mark style="color:yellow;"><code>wevtutil gp Microsoft-Windows-Security-Auditing /ge:true</code></mark></td><td>Gets the audit policy settings for the Security log using wevtutil.</td></tr><tr><td><mark style="color:yellow;"><code>secedit /export /cfg C:\auditpolicy.txt</code></mark></td><td>Exports the security settings, including audit policies, to a text file.</td></tr><tr><td><mark style="color:yellow;"><code>Get-GPOReport -All -ReportType Xml -Path C:\GPOAuditReport.xml</code></mark></td><td>Generates a report of all Group Policy Objects, including audit policy settings, in XML.</td></tr><tr><td><mark style="color:yellow;"><code>gpresult /H C:\GPOReport.html /SCOPE COMPUTER</code></mark></td><td>Generates an HTML report that includes the results of Group Policy application, which covers audit policies for the computer.</td></tr></tbody></table>

Shows the logging settings for the current firewall profile, which can indirectly relate to auditing network activities:

```powershell
netsh advfirewall show currentprofile logging
```

Filters the Security event log for events with ID 4719, which indicate changes to audit policy settings.

```powershell
Get-WinEvent -LogName "Security" | Where-Object { $_.Id -eq 4719 }
```

Retrieves the 50 most recent security events with Event ID 4719, indicating changes to audit policies.

```powershell
Get-EventLog -LogName Security -Newest 50 | Where-Object { $_.EventID -eq 4719 }
```

## <mark style="color:red;">Modify</mark>

Disables auditing for all subcategories under Logon/Logoff:

```powershell
auditpol /set /category:"Account Logon" /success:disable /failure:disable
```

Enables both success and failure auditing for the Logon events:

```powershell
auditpol /set /subcategory:"Credential Validation" /success:enable /failure:enable
```

Deletes (resets) audit policy settings for all subcategories to default values.

```powershell
auditpol /delete /subcategory:"*"
```

Uses PowerShell to enable success auditing and disable failure auditing for Account Management.

```powershell
Set-AuditPolicy -Category "Account Logon" -Success Enable -Failure Disable
```

Sets success and failure auditing for the Logon subcategory using PowerShell:

```powershell
Set-AuditPolicy -SubCategory "Credential Validation" -Success Failure
```

Enables auditing for all subcategories for both success and failure events using PowerShell:

```powershell
Set-AuditPolicy -All -Success:enable -Failure:enable
```

Backs up the current audit policy settings to a file.

```powershell
auditpol /backup /file:C:\auditpol_backup.txt
```

Restores audit policy settings from a backup file.

```powershell
auditpol /restore /file:C:\audit_policy_backup.txt
```

## <mark style="color:purple;">Audit Policy Categories and Sub-Categories</mark>

The audit categories and subcategories in Windows are part of the Advanced Audit Policy Configuration, which allows administrators to get more granular with their audit policies.

Here's a summary of the main categories and some of their subcategories as of my last update:

### <mark style="color:purple;">Account Logon</mark>

Credential Validation

Kerberos Service Ticket Operations

Kerberos Authentication Service

Other Account Logon Events

### <mark style="color:purple;">Account Management</mark>

Computer Account Management

Security Group Management

Distribution Group Management

Application Group Management

Other Account Management Events

User Account Management

### <mark style="color:purple;">Detailed Tracking</mark>

DPAPI Activity

Process Creation

Process Termination

RPC Events

### <mark style="color:purple;">DS Access</mark>

Directory Service Access

Directory Service Changes

Directory Service Replication

Detailed Directory Service Replication

### <mark style="color:purple;">Logon/Logoff</mark>

Account Lockout

IPsec Main Mode

IPsec Quick Mode

IPsec Extended Mode

Special Logon

Logoff

Logon

Network Policy Server

Other Logon/Logoff Events

User / Device Claims

### <mark style="color:purple;">Object Access</mark>

Application Generated

Certification Services

Detailed File Share

File Share

File System

Filtering Platform Connection

Filtering Platform Packet Drop

Handle Manipulation

Kernel Object

Other Object Access Events

Registry

SAM

### <mark style="color:purple;">Policy Change</mark>

Audit Policy Change

Authentication Policy Change

Authorization Policy Change

MPSSVC Rule-Level Policy Change

Filtering Platform Policy Change

Other Policy Change Events

### <mark style="color:purple;">Privilege Use</mark>

Non-Sensitive Privilege Use

Other Privilege Use Events

Sensitive Privilege Use

### <mark style="color:purple;">System</mark>

IPsec Driver

Other System Events

Security State Change

Security System Extension

System Integrity

### <mark style="color:purple;">Global Object Access Auditing</mark>

File System

Registry

Each category and subcategory provides specific events that can be audited to give administrators insight into the security and operations of a Windows environment.

The availability of certain categories and subcategories can depend on the version of Windows you are using.
