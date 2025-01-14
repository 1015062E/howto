<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

[Reporting Services uses System.Data.SqlClient to connect to the Database Engine that hosts the report server database.](https://learn.microsoft.com/en-us/sql/reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager?view=sql-server-ver16#:~:text=Reporting%20Services%20uses%20System.Data.SqlClient%20to%20connect%20to%20the%20Database%20Engine%20that%20hosts%20the%20report%20server%20database.)

[System.Data.SqlClient Namespace](https://learn.microsoft.com/en-us/dotnet/api/system.data.sqlclient?view=net-8.0)

## Prerequisites

- PowerShell installed on your machine
- SQL Server instance running (in this example, we'll use `localhost`)
- Necessary permissions to access the SQL Server database

## PowerShell Script

Below is a PowerShell script that tests the connection to a SQL Server database and retrieves the SQL Server version.

```powershell
# Create a new SQL connection object
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection

# Set the connection string
$sqlConnection.ConnectionString = "Server=localhost;Database=master;Integrated Security=SSPI;"

# Create a new SQL command object
$command = New-Object System.Data.SqlClient.SqlCommand("select @@version", $sqlConnection)

# Open the SQL connection
$sqlConnection.Open()

# Create a new SQL data adapter object
$adapter = New-Object System.Data.SqlClient.SqlDataAdapter $command

# Create a new dataset object
$dataset = New-Object System.Data.DataSet

# Fill the dataset with the result of the SQL query
$adapter.Fill($dataset) | Out-Null

# Close the SQL connection
$sqlConnection.Close()

# Output the result
$dataset.Tables
```

This script provides a simple way to test the connection to a SQL Server database using PowerShell and the `System.Data.SqlClient` namespace. You can modify the script to suit your needs, such as changing the query or the connection string to connect to a different database.

Happy scripting! 🚀
