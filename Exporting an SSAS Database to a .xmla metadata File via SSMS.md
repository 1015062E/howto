<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

## Steps to Export SSAS Database metadata(schema)

1. **Open SSMS**: Launch [SQL Server Management Studio](https://aka.ms/ssmsfullsetup) and connect to your Analysis Services instance.

2. **Connect to the Database**: In the Object Explorer, expand the server node and then the Databases node to find your SSAS database.

3. **Script the Database**:
   - Right-click on the database you want to export.
   - Select **Script Database As** > **CREATE To** > **File**.
   - Choose a location to save the .xmla file and provide a name for the file.

![image](https://github.com/user-attachments/assets/b627718e-47ca-4985-acb4-400c937b8ead)

4. **Save the Script**: The script will be generated and saved as a .xmla file at the specified location.

This process will create an XMLA script that can be used to recreate the SSAS database schema. Note that this script does not include data, only the metadata (schema) of the database.
