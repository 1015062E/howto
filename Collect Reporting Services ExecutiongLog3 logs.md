[Collect Reporting Services ExecutiongLog3 logs.md](https://github.com/guoqingsun-msft/guoqingsun/blob/main/Reporting%20Services/Collect%20Reporting%20Services%20ExecutiongLog3%20logs.md)


##### Determine which server and database engine service hosts the ExecutiongLog3 of your Reporting Services with Report Server Configuration Manager. 
![image](https://user-images.githubusercontent.com/85205970/200437891-f7d09ee9-264c-49eb-820f-3061c75d268e.png)

 
##### Connect to the database via [SQL Server Management Studio (SSMS)](https://aka.ms/ssmsfullsetup)

##### Get the reports Execution records by executing below SQL Query in SSMS
(Note: Select the ReportServer DB first before running query below. The screenshot as above highlighed in red shows your catalog DB name)

```sql
SELECT * FROM [dbo].[ExecutionLog3]
```

##### Save the output as a .CSV file (CSV please , instead of other format because it would be much easier for us to import the data to our SQL Engine Database for analysis)
Please **COMPRESS** the exported file to a .zip before uploading to the provided FTP File Transfer workspace. Thanks. 
<br>
<br>**COMPRESS** the file to a .zip before you upload, please. :)
