# Environment info
```
set
```

# Version information / kernel version
```
cat /etc/issue
uname -a
cat /proc/version
```

# Sys calls
```
/usr/include /i386-linux-gnu/asm/unistd_32.h
```

# Kernel tuning
Temporary:
```
sysctl
```

Permanent:
```
/etc/sysctl.conf
```

View configuration:
```
sysctl -a |less
```

View  configuration files for the installed modprobe modules:
```
ls -l /etc/modprobe.d/
ls -R /lib/modules/$( uname -r )/kernel
```

# Kernel module management
Insert module:
```
insmod
```

Remove module:
```
modprobe -r
rmmod
```

List modules:
```
modprobe -l
lsmod
```
