# Configuration files
```
host.conf
resolv.conf
named.conf
```

# Order of name resolution
```
/etc/nsswitch.conf
```

# DNS sever Information
```
/etc/resolv.conf
```

# Zone Transfers
```
host -t axfr domain.name dns-server
dig axfr @dns-server domain.name
```

# nslookup
```
> set type=a
> google.com

> server ns1.google.com
> google.com
```

# dig
```
Usage:  dig [@global-server] [domain] [q-type] [q-class] {q-opt}
            {global-d-opt} host [@local-server] {local-d-opt}
            [ host [@local-server] {local-d-opt} [...]]

dig google.com
dig google.com mx
dig @ns1.google.com google.com
```

Reverse lookup:
- write the IP-address in reverse order (for e.g. 192.168.1.1 will be 1.1.168.192)
- append “.in-addr.arpa.” to it.

```
dig 1.1.168.192.in-addr.arpa. PTR
```

Zone Transfer:
```
dig axfr @dns-server domain.name
```

# fierce
- scanner that helps locate non-contiguous IP space and hostnames against specified domains.
- pre-cursor to nmap, unicornscan, nessus, nikto, etc, since all of those require that you already know what IP space you are looking for
- GitHub: https://github.com/davidpepper/fierce-domain-scanner

General checks:
```
fierce -dns example.com
```

Wordlist attack:
```
fierce -dns example.com -wordlist hosts.list
```

# References
- Payload Delivery Over DNS: https://github.com/no0be/DNSlivery
- DNS Rebind Toolkit https://github.com/Kinimiwar/dns-rebind-toolkit
