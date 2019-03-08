# Versions

| SMB Version     | Windows version     |
| :-------------- | :------------------ |
| CIFS | Microsoft Windows NT 4.0 |
| SMB 1.0 | Windows 2000, Windows XP, Windows Server 2003 and Windows Server 2003 R2 |
| SMB 2.0 | Windows Vista & Windows Server 2008 |
| SMB 2.1 | Windows 7 and Windows Server 2008 R2 |
| SMB 3.0 | Windows 8 and Windows Server 2012 |
| SMB 3.0.2 | Windows 8.1 and Windows Server 2012 R2 |
| SMB 3.1.1 | Windows 10 and Windows Server 2016 |

# Ports

netbios-ns `137/tcp` # NETBIOS Name Service
netbios-ns `137/udp`
netbios-dgm `138/tcp` # NETBIOS Datagram Service
netbios-dgm `138/udp`
netbios-ssn `139/tcp` # NETBIOS session service
netbios-ssn `139/udp`
microsoft-ds `445/tcp` # if you are using Active Directory

# mblookup

NetBIOS over TCP/IP client used to lookup NetBIOS names

# Samba Enumeration
```
#!/bin/sh
#Author: rewardone
#Description:
# Requires root or enough permissions to use tcpdump
# Will listen for the first 7 packets of a null login
# and grab the SMB Version
#Notes:
# Will sometimes not capture or will print multiple
# lines. May need to run a second time for success.
if [ -z $1 ]; then echo "Usage: ./smbver.sh RHOST {RPORT}" && exit; else rhost=$1; fi
if [ ! -z $2 ]; then rport=$2; else rport=139; fi
tcpdump -s0 -n -i tap0 src $rhost and port $rport -A -c 7 2>/dev/null | grep -i "samba\|s.a.m" | tr -d '.' | grep -oP 'UnixSamba.*[0-9a-z]' | tr -d '\n' & echo -n "$rhost: " &
echo "exit" | smbclient -L $rhost 1>/dev/null 2>/dev/null
echo "" && sleep .1
```


```
nmblookup -A $ip
```

Wrapper for `smbclient`, `rpcclient`, `net` and `nmblookup`:=
```
enum4linux -a $ip
```

NSE scripts:
```
locate .nse | grep smb
```

SAMBA version number using the SMB OS discovery script:
```
nmap -A $ip -p139
```

## smbmap
```
smbmap -H $ip
```

Recursively list dirs, and files:
```
smbmap -R $sharename -H $ip
```

Downloads a file in quiet mode:
```
smbmap -R $sharename -H $ip -A $fileyouwanttodownload -q
```

> https://www.youtube.com/watch?v=jUc1J31DNdw&t=445s
