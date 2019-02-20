# Tools

- BeRoot: https://github.com/AlessandroZ/BeRoot/tree/master/Linux

# File Permissions

* Check file permissions of /etc/passwd and /etc/shadow

Find writable files
```
find -type f -maxdepth 1 -writable
```

Generate password hash (md5):
```
openssl passwd -1
```
```
echo 'joske' | openssl passwd -1 -stdin
```

Generate password hash (sha256):
```
python -c "import crypt; print crypt.crypt('joske')"
```

# SUID / SGID Binaries

Find SUID
```
find "$DIRECTORY" -perm /4000
```

Find GUID
```
find "$DIRECTORY" -perm /2000
```

Find SUID / SGID
```
find "$DIRECTORY" -perm /6000
```

Find and ls SUID / SGID
```
find "$DIRECTORY" -perm /6000 -exec ls -la {} \;
```

# Searching world writable files
```
find / -perm -w ~ -type l -ls 2?/dev/null
```

# Important Payloads

- Mempodipper compiled (Ubuntu 11 -> gimmeroot.c)

# Exploits

- Ubuntu (<= 18.10) - Dirty Sock: https://shenaniganslabs.io/2019/02/13/Dirty-Sock.html

# References

- Linux Local Privilege Escalation via SUID /proc/pid/mem Write - https://git.zx2c4.com/CVE-2012-0056/about/
