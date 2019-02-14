# Enumeration

TCP: `nmap -sS -sV -sC -n [IP]`
UDP: `nmap -sU -sV -n --top-ports 200 [IP]`
SNMP (UDP 161): `snmp-check -t [IP] -c public`
SMB (TCP 139/TCP 445): `enum4linux [IP]`
Nikto: `nikto -h http(s)://[IP]:[PORT]/[DIRECTORY]`
WebDav: `davtest -url http(s)://[IP]`

FTP (anonymous):
```
ftp [IP]
Username: anonymous Password: anonymous
```

SMB (anonymous)
```
smbclient -L \\[IP]
Username: root Password: None
```

https://github.com/furrukhtaj/Enumerator

# Scripts from awansec
https://awansec.com/oscp-review.html
