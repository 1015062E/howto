<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

How to check the version of your SQL Server Analysis Services (SSAS) using SQL Server Management Studio (SSMS), determine if the product version is still within Microsoft's support lifecycle.

### 1. Checking SSAS Version Using SSMS

To check the version of your SSAS instance using SSMS, follow these steps:

1. Open SQL Server Management Studio [SSMS](https://aka.ms/ssmsfullsetup).
2. Connect to the SSAS instance.
3. The version of your SSAS instance will be displayed as below (Note down the version number and determine its SP and CU with below links).<br>
![image](https://github.com/1015062E/howto/assets/160798406/2f4f4158-34e7-41ef-9792-84839d54e462)<br>
[SQL Server 2016 build versions](https://learn.microsoft.com/en-US/troubleshoot/sql/releases/sqlserver-2016/build-versions) | [SQL Server 2017 build versions](https://learn.microsoft.com/en-US/troubleshoot/sql/releases/sqlserver-2017/build-versions) | [SQL Server 2019 build versions](https://learn.microsoft.com/en-US/troubleshoot/sql/releases/sqlserver-2019/build-versions) | [SQL Server 2022 build versions](https://learn.microsoft.com/en-US/troubleshoot/sql/releases/sqlserver-2022/build-versions)

### 2. Determining if the Product Version is Within Microsoft Support Lifecycle

To determine if your product version is still within the Microsoft support lifecycle, you can visit the one of below pages accordingly. 
1. [SQL Server 2016 Lifecycle](https://learn.microsoft.com/en-us/lifecycle/products/sql-server-2016)
2. [SQL Server 2017 Lifecycle](https://learn.microsoft.com/en-us/lifecycle/products/sql-server-2017)
3. [SQL Server 2019 Lifecycle](https://learn.microsoft.com/en-us/lifecycle/products/sql-server-2019)
4. [SQL Server 2022 Lifecycle](https://learn.microsoft.com/en-us/lifecycle/products/sql-server-2022)



### 3. Upgrading SSAS with Backup First if your SSAS is now out of support
Refer to [Backing Up a Multidimensional or a Tabular Database](https://learn.microsoft.com/en-us/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases?view=asallproducts-allversions#bkmk_cube) before upgrading your SSAS to a version within support.

### 4. Download Link for the Latest Version
1. [SQL Server 2016 build versions](https://learn.microsoft.com/en-US/troubleshoot/sql/releases/sqlserver-2016/build-versions)
2. [SQL Server 2017 build versions](https://learn.microsoft.com/en-US/troubleshoot/sql/releases/sqlserver-2017/build-versions)
3. [SQL Server 2019 build versions](https://learn.microsoft.com/en-US/troubleshoot/sql/releases/sqlserver-2019/build-versions)
4. [SQL Server 2022 build versions](https://learn.microsoft.com/en-US/troubleshoot/sql/releases/sqlserver-2022/build-versions)

This guide is intended to be a starting point and does not cover all possible scenarios or complexities that might be involved in your specific situation.
