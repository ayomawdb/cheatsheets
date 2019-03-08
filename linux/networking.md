# Change IP
```
ifconfig eth0 192.168.1.115
ifconfig eth0 192.168.1.115 netmask 255.255.255.0 broadcast 192.168.1.255
```

# Network Information
```
netstat -­‐antp | grep sshd
```

# DHCP

Check `DHCP` page in `protocols` dir.

# DNS

Check `DNS` page in `protocols` dir.

# AF_UNIX
Used to communicate between processes on the same machine

# AF_INET and AF_INET6
Used for processes to communicate over a network connection.

# Interact with AF_UNIX Socket
```
nc -U /run/snapd.socket
GET / HTTP/1.1
Host: 127.0.0.1

```

# Tools
- Ship: https://null-byte.wonderhowto.com/how-to/linux-basics-for-aspiring-hacker-using-ship-for-quick-handy-ip-address-information-0181593/
