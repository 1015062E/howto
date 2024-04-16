>**Please refer to this document at your own discretion and understanding of potential risks involved.**

<br>MS Official doc on how to [Find the product key for SQL Server Reporting Services](https://learn.microsoft.com/en-us/sql/reporting-services/install-windows/find-reporting-services-product-key-ssrs?view=sql-server-ver15). Below steps detailed the first method introduced in the doc. It helps if your SQL Server was installed with pay-as-you-go when creating a new Azure VM. 

0.The quickest way to get the key is opening file _C:\SQLServerFull\x64\DefaultSetup.ini_ with notepad, you'll find the product key (PID).

1.Run SQL Server setup
<br>![image](https://github.com/1015062E/howto/assets/160798406/671d10bb-88b3-49cb-98ac-c1db138d9241)

2.Click on install new instance
<br>![image](https://github.com/1015062E/howto/assets/160798406/371b0456-4bbb-41e1-98c8-0d3bbf802833)

3.Copy the prepopulated key:
<br><img width="597" alt="image" src="https://github.com/1015062E/howto/assets/160798406/d1830ff6-5513-4369-a7e0-33f98a239fe9">

4.Exit the setup
