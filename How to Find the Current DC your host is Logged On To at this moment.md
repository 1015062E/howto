# How to Find the Current DC your host is Logged On To at this moment

The command that we will use is:

```batch
for /f "usebackq tokens=*" %i in (`echo %USERDNSDOMAIN%`) do nltest /dsgetdc:%i
```

This command combines two commands using the `for` command. The first command is `echo %USERDNSDOMAIN%`, which returns the fully qualified domain name (FQDN) of the current domain. The second command is `nltest /dsgetdc`, which finds a domain controller for the specified domain. The `for` command iterates over the output of the first command and passes it as input to the second command.

## The output

The output of the command will look something like this:

```batch
C:\Users\guoqingsun>for /f "usebackq tokens=*" %i in (`echo %USERDNSDOMAIN%`) do nltest /dsgetdc:%i

C:\Users\guoqingsun>nltest /dsgetdc:example.com
DC: \\DC01.example.com
Address: \\192.168.1.10
Dom Guid: 5cb2a0a1-8c93-4c4d-9f37-3d27f9f6be8e
Dom Name: example.com
Forest Name: example.com
Dc Site Name: Default-First-Site-Name
Our Site Name: Default-First-Site-Name
Flags: PDC GC DS LDAP KDC TIMESERV WRITABLE DNS_DC DNS_DOMAIN DNS_FOREST CLOSE_SITE FULL_SECRET WS DS_10
The command completed successfully
```

The output shows various information about the domain controller, such as its name, address, site, and flags. You can use this information to verify that the domain controller is working properly or troubleshoot any issues.
