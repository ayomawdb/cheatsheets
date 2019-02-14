# General
```
nc -‐nv 192.168.11.215 25
```

# "HELP" Command

# "VRFY" Command:

```
  VRFY existing_user
  Results in: 250

  VRFY nonexisting_user
  Results in: 550

  for user in $(cat users.txt); do echo VRFY $user | nc -nv -w <ip> 25 2>/dev/null | grep ^"250"; done
```
