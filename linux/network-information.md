netstat -­‐antp | grep sshd

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
