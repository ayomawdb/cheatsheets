# Server Message Block (SMB) Versions

- SMB1 - Windows 2000, XP and Windows 2003
- SMB2 - Windows Vista SP1 and Windows 2008
- SMB2.1 - Windows 7 and Windows 2008 R2
- SMB3 - Windows 8 and Windows 2012

`135`, `137` -
`445`- SMB over IP (used when SMB is used directly on TCP stack, without using NetBIOS)
`139`- NBT over IP

# Scanning
```
nmap --script smb-protocols -p44 (target/range)
```
```
nmap -p 139,446 <ip-range> --open
```
```
nbtstat <ip>
nbtscan -‐r 192.168.11.0/24
```
```
enum4linux -‐a 192.168.11.227
```
```
nmap ‐v ‐p 139, 445 -‐script=smb‐security‐mode 192.168.11.236
nmap ‐v ‐p 139, 445 -‐script=smb‐os-discovery 192.168.11.227
nmap ‐v ‐p 139, 445 -‐script=smb‐check-vulns --script-args=unsafe=1 192.168.11.227
```

# Enable / Disable / Status

> Detect, enable and disable SMBv1, SMBv2, and SMBv3 in Windows and Windows Server: https://support.microsoft.com/en-gb/help/2696547/how-to-detect-enable-and-disable-smbv1-smbv2-and-smbv3-in-windows-and

## Windows Server 2012 R2 & 2016: PowerShell methods
### SMB v1
- Detect: `Get-WindowsFeature FS-SMB1`
- Disable: `Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol`
- Enable: `Enable-WindowsOptionalFeature -Online -FeatureName smb1protocol`

### SMB v2/v3
- Detect: `Get-SmbServerConfiguration | Select EnableSMB2Protocol`
- Disable: `Set-SmbServerConfiguration -EnableSMB2Protocol $false`
- Enable: `Set-SmbServerConfiguration -EnableSMB2Protocol $true`

## Windows 8.1 and Windows 10: PowerShell method
### SMB v1 Protocol
- Detect:	`Get-WindowsOptionalFeature –Online –FeatureName SMB1Protocol`
- Disable:	`Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol`
- Enable:	`Enable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol`

### SMB v2/v3 Protocol
- Detect:	`Get-SmbServerConfiguration | Select EnableSMB2Protocol`
- Disable: `Set-SmbServerConfiguration –EnableSMB2Protocol $false`
- Enable:	`Set-SmbServerConfiguration –EnableSMB2Protocol $true`

## Windows 8 and Windows Server 2012
### SMB v1 on SMB Server
- Detect:	`Get-SmbServerConfiguration | Select EnableSMB1Protocol`
- Disable:	`Set-SmbServerConfiguration -EnableSMB1Protocol $false`
- Enable:	`Set-SmbServerConfiguration -EnableSMB1Protocol $true`

### SMB v2/v3 on SMB Server
- Detect:	`Get-SmbServerConfiguration | Select EnableSMB2Protocol`
- Disable:	`Set-SmbServerConfiguration -EnableSMB2Protocol $false`
- Enable:	`Set-SmbServerConfiguration -EnableSMB2Protocol $true`

##  Windows 7, Windows Server 2008 R2, Windows Vista, and Windows Server 2008
### SMB v1 on SMB Server
Default configuration = Enabled (No registry key is created), so no SMB1 value will be returned

- Detect: `Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}`
- Disable: `Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 0 –Force`
- Enable: `Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 1 –Force`

### SMB v2/v3 on SMB Server
- Detect: `Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}``
- Disable: `Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 0 –Force`
- Enable: `Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 1 –Force`

## Disable SMB Client
### SMB v1 on SMB Client
- Detect:	`sc.exe qc lanmanworkstation`
- Disable:
```
sc.exe config lanmanworkstation depend= bowser/mrxsmb20/nsi
sc.exe config mrxsmb10 start= disabled
```
- Enable:
```
sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
sc.exe config mrxsmb10 start= auto
```

### SMB v2/v3 on SMB Client
- Detect:	`sc.exe qc lanmanworkstation`
- Disable:
```
sc.exe config lanmanworkstation depend= bowser/mrxsmb10/nsi
sc.exe config mrxsmb20 start= disabled
```
- Enable:
```
sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
sc.exe config mrxsmb20 start= auto
```

# Null Session Enumeration

Null Session Enumeration (enabled by default in SMB1)

```
rpcclient -U "" ip (give empty password)
  > srvinfo
  > enumdomusers
  > getdompwinfo
```

# Tools

- nbtstat
- nbtscan
- enum4linux
- rpcclient

# Samba Configuration
Configuration file:
```
/etc/samba/smb.conf
```

Test & reload configuration
```
testparm -v
service smb restart
```

User creation:
```
smbpasswd -a <username>
```
