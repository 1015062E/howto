```markdown
# Testing Connection to SQL Server using System.Data.SqlClient with PowerShell

In this blog post, we'll walk through how to test a connection to a SQL Server database using the `System.Data.SqlClient` namespace in PowerShell. This can be particularly useful for verifying connectivity and troubleshooting connection issues.

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

## Explanation

1. **Creating the SQL Connection**: We start by creating a new SQL connection object and setting the connection string to connect to the `master` database on `localhost` using integrated security.

2. **Executing the SQL Command**: We create a new SQL command object with the query `select @@version` to get the SQL Server version.

3. **Opening the Connection**: The connection to the SQL Server is opened.

4. **Filling the Dataset**: We use a SQL data adapter to execute the command and fill the dataset with the result.

5. **Closing the Connection**: The connection to the SQL Server is closed.

6. **Outputting the Result**: Finally, we output the result stored in the dataset.

## Conclusion

This script provides a simple way to test the connection to a SQL Server database using PowerShell and the `System.Data.SqlClient` namespace. You can modify the script to suit your needs, such as changing the query or the connection string to connect to a different database.

Feel free to share this script with others who might find it useful!

---

Happy scripting! 🚀
```
