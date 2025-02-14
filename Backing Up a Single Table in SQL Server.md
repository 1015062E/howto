<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

**Disclaimer:** This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Backing Up a Single Table in SQL Server

When working with Microsoft SQL Server, you may find yourself in a situation where you need to back up only a single table rather than the entire database. SQL Server's built-in `BACKUP DATABASE` command does not support backing up individual tables, but there are multiple workarounds to achieve this. This guide covers several methods to export and restore a single table in SQL Server.

### Exporting a Single Table

#### Use BCP (Bulk Copy Program) to Export Table Data
The `bcp` utility allows exporting and importing table data efficiently.

**Export Table Data to a File:**
```sh
bcp [YourDatabase].[dbo].[YourTable] out "C:\Backup\YourTable.bcp" -c -T -S YourServer
```

**Breakdown of the Command:**
- `[YourDatabase].[dbo].[YourTable]` – Replace with your actual database and table name.
- `out "C:\Backup\[YourTable].bcp"` – Path where the data will be stored.
- `-c` – Uses character data format.
- `-T` – Uses a trusted connection (Windows Authentication).
- `-S YourServer` – Replace with your actual SQL Server instance name.

**Import Table Data Back into SQL Server:**
```sh
bcp [YourDatabase].[dbo].[YourTable] in "C:\Backup\YourTable.bcp" -c -T -S YourServer
```

### Finding Your SQL Server Instance Name
If you're unsure about your server name for the `-S` parameter in `bcp`, run this in SSMS:
```sql
SELECT @@SERVERNAME;
```
- If using the **default instance**, use:
  ```sh
  -S localhost
  ```
- If using a **named instance**, use:
  ```sh
  -S ServerName\InstanceName
  ```
- If using a **remote server**, use:
  ```sh
  -S 192.168.1.100
  ```

### Running `bcp` in PowerShell or Command Prompt
You can run the `bcp` command in either **PowerShell** or **Command Prompt (cmd)**:
```powershell
bcp [YourDatabase].[dbo].[YourTable] out "C:\Backup\YourTable.bcp" -c -T -S YourServer
```
If `bcp` is not recognized, run it using the full path:
```powershell
& "C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\XX\Tools\Binn\bcp.exe" [YourDatabase].[dbo].[YourTable] out "C:\Backup\YourTable.bcp" -c -T -S YourServer
```
Replace `XX` with your SQL Server version (e.g., `150` for SQL Server 2019).
