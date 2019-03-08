# Find name servers
```
host -t ns $ip
```
# Find email servers
```
host -t mx $ip
```

# Subdomain bruteforcing
```
for ip in $(cat list.txt); do host $ip.$website; done
```

# Reverse dns lookup bruteforcing
```
for ip in $(seq 155 190);do host 50.7.67.$ip;done |grep -v "not found"
```

# Zone transfer request
```
host -l $ip ns1.$ip
```
```
dnsrecon -d $ip -t axfr
```

# Finds nameservers for a given domain
```
host -t ns $ip| cut -d " " -f 4 #
```
```
dnsenum $ip
```

# Nmap zone transfer scan
```
nmap $ip --script=dns-zone-transfer -p 53
```

# Finds the domain names for a host.
```
whois $ip
```

# Find the IP and authoritative servers.
```
nslookup $ip
```

# Finds miss configure DNS entries.
```
host -t ns $ip
```

# TheHarvester finds subdomains in google, bing, etc
```
python theHarvester.py  -l 500 -b all -d $ip
```
