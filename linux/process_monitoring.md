ltrace
strace
access

The check is done using the calling process's real UID and GID,
     rather than the effective IDs as is done when actually attempting an
     operation (e.g., open(2)) on the file.

Check permissions for the UID and GID of the process (executable file owner / group)
