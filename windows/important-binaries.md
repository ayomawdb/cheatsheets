# wbadmin / ntbackup

> https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wbadmin

Perform backups and restores of operating systems, drive volumes, computer files, folders, and applications from a command-line interface.

Delete any recovery catalogs:
```
cmd.exe /c wbadmin.exe delete catalog -quiet
```

# BCDEdit

> https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/bcdedit-command-line-options

Tool for managing Boot Configuration Data (BCD). BCD files provide a store that is used to describe boot applications and boot application settings.

Usable to creating new stores, modifying existing stores, adding boot menu options, and so on.

Windows recovery console does not attempt to repair anything:
```
cmd.exe /c bcdedit.exe /set {default} bootstatuspolicy ignoreallfailures & bcdedit /set {default} recoveryenabled no
```

# wevtutil

> https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil

Enables you to retrieve information about event logs and publishers. You can also use this command to install and uninstall event manifests, to run queries, and to export, archive, and clear logs.

Clear System and Security logs:
```
cmd.exe /c wevtutil.exe cl System
cmd.exe /c wevtutil.exe cl Security
```

# DUMPBIN

> https://docs.microsoft.com/en-us/cpp/build/reference/dumpbin-reference?view=vs-2017

Displays information about Common Object File Format (COFF) binary files. You can use DUMPBIN to examine COFF object files, standard libraries of COFF objects, executable files, and dynamic-link libraries (DLLs).
