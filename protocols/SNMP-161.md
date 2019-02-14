# Simple Network Management Protocol (SNMP)

- Baed on UDP - Can be suspectable for IP spoofing and replay
- 1,2,2c versions are plain text
- Week auth and default community strings (public, default)

Devices often support configuration file read and write through private SNMP community string access. Hence having access to private string means router configuration can be altered.

# SNMP - Management Information Base (MBI)

Tree database related to network management.
http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.progcomm/doc/progcomc/mib.htm

commuity strings - public / private / manager / ...

# Scanning
```
nmap -sU --open -p 161 <ip> --open
```
Scan one community string for multiple IPs
```
onesixtyone -c community.txt -i ips.txt
```

# Probe MBI
```
snmpwalk -c public -v1 <ip> 1.3.6.1.2.1.25.4.2.1.2
 • 1.3.6.1.2.1.25.1.6.0 System Processes
 • 1.3.6.1.2.1.25.4.2.1.2 Running Programs
 • 1.3.6.1.2.1.25.4.2.1.4 Processes Path
 • 1.3.6.1.2.1.25.2.3.1.4 Storage Units
 • 1.3.6.1.2.1.25.6.3.1.2 Software Name
 • 1.3.6.1.4.1.77.1.2.25 User Accounts
 • 1.3.6.1.2.1.6.13.1.3	 TCP Local Ports
```

# Tools

- snmpwalk
- snmpenum
- snmpcheck
- onesixtyone
  - Scan one community string for multiple IPs
