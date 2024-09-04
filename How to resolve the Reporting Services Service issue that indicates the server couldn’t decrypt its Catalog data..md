<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

<Applies to : On-prem SQL Server Reporting Services 2016 and ealier, SSRS 2017 and later, Power BI Report Server>

How to resolve the Reporting Services Service/Report Server issue that indicates the report server couldn’t decrypt those encrypted data in the database(ReportServer Catalog)? You might receive below error message when you come across such issue. 

- The report server was unable to validate the integrity of encrypted data in the database.
- The report server can’t access or use the encryption key. You might need to add the server to the scale-out group, reimport encrypted content, or delete all encrypted content and generate a new encryption key.

**Note** : To view and reconfigure Reporting Services service, always use the **Reporting Services Configuration Manager**(it's **Report Server Configuration Manager** in newer RS versions). 

1.	If your Reporting Services service is in a scaled out deployment group, however there's no issue with other instance(s). Take a Encryption Key backup from the working instance and restore to the non-working one. (How-to? - [SSRS Encryption Keys - Back Up and Restore Encryption Keys](https://learn.microsoft.com/en-us/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys?view=sql-server-ver16))
2.	Else confirm internally with your team if they have ever backed up the Encryption Key(a file with .snk extension) for the Reporting Services Service in question. If yes, get the file and restore for the RS instance (Open Reporting Services Configuration Manager , click on ‘Encryption Keys’, then ‘Restore’. You may refer to [Restore encryption keys -Report Server Configuration Manager (Native Mode)](https://learn.microsoft.com/en-us/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys?view=sql-server-ver16#bkmk_restore_configuration_manager))
3.	If unfortunately, your team didn’t ever backup the Encryption Key. Confirm if the issue appeared after your team changed the Service Account by accident via Services.msc console ? If yes, change the service account back to previous one. Then check if RS is back to normal. If yes, take Encryption Key backup and then proceed with changing the account to the one you want use **Reporting Services Configuration Manager**.
4.	Else if the RS service is migrated from another instance ? If yes, is that old instance is still available now ? If yes, get(‘backup’) the encryption key from that RS instance and restore on the problematic instance. 
5.	Else if the instance is a new one and there’s no important reports , try specifying a new Catalog for the new RS instance (click on ‘Database’ in RS Configuration Manager, then ‘change database’, ‘create new database’). This way you’ll get an empty RS instance (there’s no any data/reports)  ![image](https://user-images.githubusercontent.com/85205970/209743199-ba4609e3-268d-47a0-aeab-bb870a617611.png)

6.	Else if there are reports in the current RS catalog which you need them to come back available and above solutions are not applicable to you.  **As last resort**, you may have to delete all encrypted data in the database and fill in back manually via Server Portal UI.  (**Note** : Deleting the encryption keys removes all symmetric key information from the report server database and deletes any encrypted content. Please read - [Deleting Unusable Encrypted Content](https://learn.microsoft.com/en-us/sql/reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys?view=sql-server-ver16#deleting-unusable-encrypted-content))  ![image](https://user-images.githubusercontent.com/85205970/209743608-8ff5e1d1-298d-435a-a9ff-a9924d61196e.png)
