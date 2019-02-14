Server   Message   Block   (SMB)

o SMB1  –  Windows  2000,  XP  and  Windows  2003
o SMB2  –  Windows  Vista  SP1  and  Windows  2008  
o SMB2.1  –  Windows  7  and  Windows  2008  R2  
o SMB3  –  Windows  8  and  Windows  2012

445  ‘SMB over IP’ (used when SMB is used durectly on TCP stack (without using NetBIOS))
139  ‘NBT over IP’

nmap -p 139,446 <ip-range> --open
nbtstat <ip>
nbtscan -­‐r 192.168.11.0/24

Null  Session  Enumeration (enabled by default in SMB1)

rpcclient -U  "" ip  (give empty password)
    > srvinfo
    > enumdomusers
    > getdompwinfo

enum4linux -­‐a 192.168.11.227

nmap  -­‐v  -­‐p  139,  445  -­‐-­‐script=smb-­‐security-­‐mode  192.168.11.236
nmap  -­‐v  -­‐p  139,  445  -­‐-­‐script=smb-­‐os-­‐discovery  192.168.11.227
nmap  -­‐v  -­‐p  139,  445  -­‐-­‐script=smb-­‐check-­‐vulns --script-args=unsafe=1  192.168.11.227

# Tools

- nbtstat
- nbtscan
- enum4linux
- rpcclient
