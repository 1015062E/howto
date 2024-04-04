## The command

The command that we will use is:

```batch
for /f "usebackq tokens=*" %i in (`echo %USERDNSDOMAIN%`) do nltest /dsgetdc:%i
```

## The output

The output of the command will look something like this:

```batch
C:\Users\guoqingsun>for /f "usebackq tokens=*" %i in (`echo %USERDNSDOMAIN%`) do nltest /dsgetdc:%i

C:\Users\guoqingsun>nltest /dsgetdc:example.com
DC: \\DC01.example.com
Address: \\192.168.1.10
Dom Guid: <GUID>
Dom Name: example.com
Forest Name: example.com
Dc Site Name: Default-First-Site-Name
Our Site Name: Default-First-Site-Name
Flags: PDC GC DS LDAP KDC TIMESERV WRITABLE DNS_DC DNS_DOMAIN DNS_FOREST CLOSE_SITE FULL_SECRET WS DS_10
The command completed successfully
```
