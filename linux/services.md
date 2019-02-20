#Check if certain service is up:
```
update-­‐rc.d ssh enable
```

# Auto start a service:
```
update-­‐rc.d ssh enable
```

# Systemd services
```
Example:

/lib/systemd/system/snapd.service
```

# Systemd socket unit file
```
Example:

[Socket]
ListenStream=/run/snapd.socket
ListenStream=/run/snapd-snap.socket
SocketMode=0666
```
`0666` - Allow any process to connect and communicate with the socket.
