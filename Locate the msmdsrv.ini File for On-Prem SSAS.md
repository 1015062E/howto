<br>
<table>
  <td>WARNING</td>
  <td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

*Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.*

## How to Locate the msmdsrv.ini File for SSAS On-Premises

SQL Server Analysis Services (SSAS) running on on-premises servers uses the `msmdsrv.ini` file to store its configuration settings, such as memory limits and port numbers. If you need to retrieve this file—perhaps to share with a support team or review settings—locating it can seem tricky at first. This post provides step-by-step guidance to find the `msmdsrv.ini` file using tools like the Services console, SQL Server Configuration Manager, or SQL Server Management Studio (SSMS). 

For simplicity and reliability, we recommend starting with the **Services console method**, as it’s straightforward and doesn’t require additional software. The other methods are included as backup options if needed.

### Why the Config File Matters

The `msmdsrv.ini` file is an XML configuration file critical to SSAS operations. It resides in the instance’s configuration folder, and its exact location depends on the installation path and instance name (e.g., default or named). The SSAS service executable (`msmdsrv.exe`) uses a `-s` switch to point directly to this folder, making it easier to locate once you know where to look.

### Recommended Method: Using the Services Console

The Services console (`services.msc`) is the easiest way to find the `msmdsrv.ini` file because it’s built into Windows and clearly displays the configuration path via the `-s` switch.

#### Steps
1. **Open Services Console:**
   - Press `Win + R`, type `services.msc`, and press Enter.

2. **Find the SSAS Service:**
   - Look for a service named `SQL Server Analysis Services (MSSQLSERVER)` (default instance) or `SQL Server Analysis Services (INSTANCENAME)` (named instance). Replace `INSTANCENAME` with your specific instance name.

3. **Check the Path to Executable:**
   - Right-click the service and select **Properties**.
   - In the **General** tab, find the **Path to executable**. It might look like:
     ```
     "C:\Program Files\Microsoft SQL Server\MSAS16.MSSQLSERVER\OLAP\bin\msmdsrv.exe" -s "C:\Program Files\Microsoft SQL Server\MSAS16.MSSQLSERVER\OLAP\Config"
     ```
   - Note the path after the `-s` switch (e.g., `C:\Program Files\Microsoft SQL Server\MSAS16.MSSQLSERVER\OLAP\Config`).

4. **Navigate to the Folder:**
   - Open File Explorer, paste the path from after `-s` into the address bar, and press Enter.

5. **Locate the File:**
   - Inside the folder (e.g., `Config`), you’ll find `msmdsrv.ini`.

6. **Next Steps:**
   - Copy the file or open it in a text editor like Notepad. Always make a backup before editing.

---

### Backup Method 1: Using SQL Server Configuration Manager

If the Services console isn’t an option, SQL Server Configuration Manager provides a similar approach by showing the `-s` switch in the service’s binary path.

#### Steps
1. **Open Configuration Manager:**
   - Search for `SQL Server Configuration Manager` in the Start menu and open it.

2. **Locate the SSAS Service:**
   - Expand **SQL Server Services** and find `SQL Server Analysis Services (MSSQLSERVER)` or your named instance.

3. **Check the Binary Path:**
   - Right-click the service, select **Properties**, and go to the **Service** tab.
   - Look at the **Binary Path**, e.g.:
     ```
     "C:\Program Files\Microsoft SQL Server\MSAS16.MSSQLSERVER\OLAP\bin\msmdsrv.exe" -s "C:\Program Files\Microsoft SQL Server\MSAS16.MSSQLSERVER\OLAP\Config"
     ```
   - Note the path after `-s`.

4. **Navigate and Locate:**
   - In File Explorer, go to the path after `-s` and find `msmdsrv.ini`.

5. **Next Steps:**
   - Copy or back up the file as needed.

---

### Backup Method 2: Using SQL Server Management Studio (SSMS)

If you prefer using SSMS or need to verify the instance first, this method works by deriving the config folder from the data directory.

#### Steps
1. **Connect to SSAS:**
   - Open SSMS, set **Server type** to `Analysis Services`, and connect to your instance (e.g., `localhost` or `localhost\INSTANCENAME`).

2. **View Properties:**
   - Right-click the instance in Object Explorer and select **Properties**.
   - In the **General** tab, note the **DataDir** (e.g., `C:\Program Files\Microsoft SQL Server\MSAS16.MSSQLSERVER\OLAP\Data`).

3. **Derive the Config Path:**
   - Go up one level from `Data` to the `OLAP` folder, then into `Config` (e.g., `C:\Program Files\Microsoft SQL Server\MSAS16.MSSQLSERVER\OLAP\Config`).

4. **Locate the File:**
   - Find `msmdsrv.ini` in the `Config` folder.

5. **Next Steps:**
   - Copy or back up the file.

---

### Key Notes
- **Path Variations:** The `MSAS16` in the path reflects the SQL Server version (e.g., 2022). This may differ (e.g., `MSAS15` for 2019) based on your installation.
- **Permissions:** Administrative access is required to view or edit files in these directories.
- **The `-s` Switch:** This switch explicitly points to the config folder, making the Services console or Configuration Manager methods the most direct.
