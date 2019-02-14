# Using whois
```
whois example.com
whois 50.7.67.186 (reverse)
```

# Forward Lookup
```
host -t ns example.com
host -t mx example.com

host www.example.com -> results in IP address
host nonexistent.example.com -> results in not found error
```

# Reverse Lookup
```
for ip in $(seq 155 190);do host 50.7.67.$ip;done |grep -­‐v "not found"
```
> https://stackoverflow.com/questions/23981098/how-forward-and-reverse-dns-works

# Zone Transfers

Copying of the zone file from a master DNS server to a slave server
```
host -l example.com ns1.example.com
```
```
#/bin/bash
# Simple Zone Transfer Bash Script
# $1 is the first argument given after the bash script
# Check if argument was given, if not, print usage
if [ -­‐z "$1" ]; then
echo "[*] Simple Zone transfer script"
echo "[*] Usage : $0 <domain name> "
exit 0
fi

# if argument was given, identify the DNS servers for the domain
for server in $(host -­‐t ns $1 |cut -­‐d" " -­‐f4);do
# For each of these servers, attempt a zone transfer
host -­l $1 $server |grep "has address"
done
```
# DNS Related Recon Tools

## recon-ng
```
use recon/contacts/gather/http/api/whois_pocs
set DOMAIN example.com
run

use recon/hosts/enum/http/web/xssed
use recon/hosts/gather/http/web/google_site
use recon/hosts/gather/http/web/ip_neighbor
```

## dnsrecon
```
dnsrecon
dnsrecon ‐d example.com ‐t axfr

dnsenum
dnsenum example.com
```

## subbrute
- Recursively crawls enumerated DNS records
- Uses open resolvers as a kind of proxy to circumvent DNS rate-limiting

## knock
- Wordlist based subdomain bruteforcing
- Virustotal search

## Sublist3r
- Subdomains with Google, Yahoo, Bing, Baidu, Ask, Netcraft, Virustotal, ThreatCrowd, DNSdumpster, and ReverseDNS
- Can do "subbrute" scans internally
- Can do port scans internally

## Online Services
- https://dnsdumpster.com/

# DNS Recon Workflow (WIP)

1) Get the host's addresse (A record).
2) Get the namservers (threaded).
3) Get the MX record (threaded).
4) Perform axfr queries on nameservers and get BIND VERSION (threaded).
5) Get extra names and subdomains via google scraping (google query = "allinurl: -www site:domain").
6) Brute force subdomains from file
7) Calculate C class domain network ranges and perform whois queries on them (threaded).
8) Perform reverse lookups on netranges (C class or/and whois netranges) (threaded).
9) Write to domain_ips.txt file ip-blocks.
10)
