```PowerShell
[System.Data.Common.DbProviderFactories]::GetFactoryClasses()|ogv
```
![image](https://github.com/user-attachments/assets/6b58dc60-331e-4a55-8071-56f5b68342f0)

```PowerShell
[System.Data.Common.DbProviderFactories]::GetFactoryClasses()
```

Retrieves a list of all the data providers installed on your system that implement the DbProviderFactory class. This command returns a DataTable containing information about each provider, such as:
- Name: The readable name of the data provider.
- Description: A description of the data provider.
- InvariantName: The programmatic name used to refer to the data provider.
- AssemblyQualifiedName: The fully qualified name of the factory class, which includes enough information to instantiate the object.

<br>Ref : https://learn.microsoft.com/en-us/dotnet/api/system.data.common.dbproviderfactories?view=net-8.0

To check if there's 32 bit or 64 bit ODAC driver installed : 

Using registry : 
```ini
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\ORACLE\KEY_ORAClient_xxxxxxxx
```

Open `%windir%\Microsoft.NET\assembly`, search `System.Data.OracleClient.dll`
![image](https://github.com/user-attachments/assets/d379d54b-f0ad-49bc-8251-5ea8405867bc)

CMD : 
```cmd
echo %PATH%
```
