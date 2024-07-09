
[Dynamic Management Views (DMVs)](https://learn.microsoft.com/en-us/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services?view=asallproducts-allversions)

1. **Start SQL Server Management Studio (SSMS)** https://aka.ms/ssmsfullsetup.
2. In the **Connect to Server** dialog box, select the **Analysis Services** server type.
3. In the **Login** tab, enter the server name by typing the name of the computer on which the server is running.
4. For a named SSAS instance, the server name must be specified in this format: `servername\\instance name`. For AAS, the name should be something like `asazure://<Region>.asazure.windows.net/<AASServiceName>`; For Power BI it's something like `powerbi://api.powerbi.com/v1.0/myorg/<workspaceName>`
5. Once connected, right-click the server or database object > **New Query** > **MDX**.
6. Type your DMV query, and then click **Execute**, or press **F5**.

```sql
SELECT * FROM $System.TMSCHEMA_TABLES
```
![image](https://github.com/1015062E/howto/assets/160798406/dcaa0aa6-308d-4022-923b-8f2a9932497c)


```sql
SELECT * FROM $System.TMSCHEMA_TABLES WHERE [ID]='10'
```
![image](https://github.com/1015062E/howto/assets/160798406/40d71288-83fa-4393-ad7f-dd8316f44754)


```sql
SELECT * FROM $SYSTEM.TMSCHEMA_PARTITIONS
```

![image](https://github.com/1015062E/howto/assets/160798406/8f07bfb8-938e-4a44-8960-751998703f0e)


```sql
SELECT * FROM $SYSTEM.TMSCHEMA_PARTITIONS WHERE [TableID]='10' AND [ID]='151'
```
![image](https://github.com/1015062E/howto/assets/160798406/b5639674-346c-4128-bee6-6c8952690096)
