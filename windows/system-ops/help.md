# Help

## <mark style="color:red;">Commands</mark>

| <mark style="color:yellow;">`Get-Help`</mark>                    | Help                       |
| ---------------------------------------------------------------- | -------------------------- |
| <mark style="color:yellow;">`Help`</mark>                        | Help with paging (better)  |
| <mark style="color:yellow;">`Get-Help <cmdlet>`</mark>           | Help                       |
| <mark style="color:yellow;">`Get-Help <cmdlet> -detailed`</mark> | Detailed help              |
| <mark style="color:yellow;">`Get-Help <cmdlet> -examples`</mark> | Usage examples             |
| <mark style="color:yellow;">`Get-Help <cmdlet> -full`</mark>     | Full help                  |
| <mark style="color:yellow;">`Get-Help <cmdlet> -online`</mark>   | Online help (if available) |
| <mark style="color:yellow;">`Help Get-EventS*`</mark>            | Supports Wildcards         |

## <mark style="color:red;">Finding Command</mark>s

### <mark style="color:purple;">Display Commands</mark>

Get cmdlets and display them in order:

```powershell
Get-Command -Type Cmdlet | Sort-Object -Property Noun | Format-Table -GroupBy Noun
```

Cleaner (by Noun):

```powershell
get-command -Type Cmdlet | Select-Object -Property Noun, Name | Sort-Object Noun | Format-Table -GroupBy Noun
```

Grid View Window:

```powershell
get-command -Type Cmdlet | Select-Object -Property Noun, Name | Sort-Object Noun | Out-GridView -Title "PowerShell Commands by Noun"
```

Get Functions:

```powershell
get-command -Type Function | Select-Object -Property Noun, Name | Sort-Object Noun | Format-Table -GroupBy Noun
```

Grid View Window:

```powershell
get-command -Type Function | Select-Object -Property Noun, Name | Sort-Object Noun | Out-GridView -Title "PowerShell Functions"
```

Get commands in a module:

```powershell
Get-Command -Module Microsoft.PowerShell.Security, Microsoft.PowerShell.Utility
```



### <mark style="color:purple;">Finding Cmdlets</mark>

| <mark style="color:yellow;">`Get-Command`</mark>               | All available cmdlets        |
| -------------------------------------------------------------- | ---------------------------- |
| <mark style="color:yellow;">`Get-Command Set*`</mark>          | Wildcard filter              |
| <mark style="color:yellow;">`Get-Command *Process`</mark>      | Wildcard filter              |
| <mark style="color:yellow;">`Get-Command –Verb Set`</mark>     | Filter cmdlets on verb "set" |
| <mark style="color:yellow;">`Get-Command –Noun process`</mark> | Filter on noun "process"     |
| <mark style="color:yellow;">`gmc`</mark>                       | Alias                        |



## <mark style="color:red;">Cmdlet Aliases</mark>

| <mark style="color:yellow;">`Get-Alias`</mark>    | Show aliases                               |
| ------------------------------------------------- | ------------------------------------------ |
| <mark style="color:yellow;">`alias gcm`</mark>    | Expand an alias                            |
| <mark style="color:yellow;">`New-Alias`</mark>    | Create custom alias                        |
| <mark style="color:yellow;">`Export-Alias`</mark> | Makes variables persistent across sessions |



