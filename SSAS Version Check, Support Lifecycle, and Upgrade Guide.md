# SSAS Version Check, Support Lifecycle, and Upgrade Guide

This article provides a comprehensive guide on how to check the version of your SQL Server Analysis Services (SSAS) using SQL Server Management Studio (SSMS), determine if the product version is still within Microsoft's support lifecycle, check if the latest version of the product main version (for example, SSAS SQL 2016), latest Service Pack (SP), and Cumulative Update (CU) are still within support. If they are, it guides you on how to upgrade SSAS with a backup first. It also provides a download link for the latest version in case the latest version is still within support.

## 1. Checking SSAS Version Using SSMS

To check the version of your SSAS instance using SSMS, follow these steps:

1. Open SQL Server Management Studio (SSMS).
2. Connect to the SSAS instance.
3. Navigate to `Reports -> Standard Reports -> General`.

The version of your SSAS instance will be displayed in the report.

## 2. Determining if the Product Version is Within Microsoft Support Lifecycle

Microsoft provides a lifecycle for each of its products, which includes SQL Server Analysis Services. To determine if your product version is still within the Microsoft support lifecycle, you can visit the [Microsoft Product Lifecycle Search page](^28^). Here, you can search for your product and view its lifecycle, including support and servicing timelines, required updates, migration information, and system requirements.

## 3. Checking if the Latest Version of the Product Main Version is Still Within Support

To verify if the latest version of the product main version, latest SP, and CU are still within support, you can compare the build version numbers of Analysis Services component files installed on your computer with the build version numbers for a particular CU. 

For example, to verify the component file version for SQL Server 2016 SP3, you can go to the [SQL Server 2016 build versions](^22^) page. In the SQL Server 2016 cumulative update (CU) builds, click the Knowledge Base Number for the build you want to verify. In the Cumulative Update (#) for SQL Server 2016 article, in the Cumulative Update package information section, expand Cumulative update package file information. In the SQL Server 2016 Analysis Services table, check the File version for the msmdsrv.exe component file. If the CU has been applied, the file version number should match the msmdsrv.exe file installed on your computer.

## 4. Upgrading SSAS with Backup First

Before upgrading your SSAS, it's crucial to back up all databases and verify that each can be restored. Here are the steps to upgrade your SSAS instance:

1. Backup all databases and verify that each can be restored. To learn more, see [Backup and restore Analysis Services databases](^16^).
2. Run Setup and specify the name of the existing instance as the name of the new instance for an in-place upgrade.
3. After the upgrade, process the databases.
4. Run databases consistency checks.
5. Test dependent applications.

## 5. Download Link for the Latest Version

If the latest version of SSAS 2016 SP3 is still within support, you can download it from the [Official Microsoft Download Center](^2^).

This guide is intended to be a starting point and does not cover all possible scenarios or complexities that might be involved in your specific situation.
