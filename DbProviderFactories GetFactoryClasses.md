```
[System.Data.Common.DbProviderFactories]::GetFactoryClasses()|ogv
```
![image](https://github.com/user-attachments/assets/6b58dc60-331e-4a55-8071-56f5b68342f0)



Retrieves a list of all the data providers installed on your system that implement the DbProviderFactory class. This command returns a DataTable containing information about each provider, such as:

Name: The readable name of the data provider.
Description: A description of the data provider.
InvariantName: The programmatic name used to refer to the data provider.
AssemblyQualifiedName: The fully qualified name of the factory class, which includes enough information to instantiate the object.

Ref : https://learn.microsoft.com/en-us/dotnet/api/system.data.common.dbproviderfactories?view=net-8.0
