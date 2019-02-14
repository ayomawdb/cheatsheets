# Memory map for a process
```
 cat /proc/1234/maps
```
```
gdb
info proc mappings
```
```
pmap -d 1234
```

# System and library calls
- `ltrace`
- `strace`

# Access control
- `access` - Check permissions for the UID and GID of the process (executable file owner / group)
  - Check is done using the calling process's real UID and GID, rather than the effective IDs as is done when actually attempting an operation (e.g., open(2)) on the file.
