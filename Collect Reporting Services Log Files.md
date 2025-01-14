
If you already know where your Reporting Services is installed, please directly go to [Step 6](https://github.com/1015062E/howto/blob/main/Collect%20Reporting%20Services%20Log%20Files.md#6to-collect-reporting-service-logs-please-select-and-compress-the-whole-logfiles-folder) down below. 

Else, please check out your Reporting Services' installation path following below steps : 
<br>Applies to : SQL Server Reporting Services(Native mode) 2016 and ealier, SSRS 2017 and later, on-prem Power BI Report Server. 

#### Here is a list of default installation folder for SQL Server Reporting Service or PowerBI Report Server. (Your Reporting Service might be installed to custom specified folder, please follow below instructions to check )
| RS Version/Env | Default installation folder |
| ------ | ------ |
| SSRS 2016 or earlier | C:\Program Files\Microsoft SQL Server\\**MSRS<Version#>.\<InstanceName>**\Reporting Services\ |
| SSRS 2017 or 2019 | C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\ |
| On-Prem Power BI Report Server | C:\Program Files\Microsoft Power BI Report Server\PBIRS\ |

##### 1).Open Services console (services.msc)
>![image](https://github.com/1015062E/howto/assets/160798406/14af6df0-c681-4cd2-9dcc-4c6c2dcb06f7)


##### 2).Find **SQL Server Reporting Services, SSRS, or Power BI Report Server**(you should know what your reporting services is). Make sure you are checking the correct instance if you have more than one. 

##### 3).Right click on the service(take SSRS as example, yours might be different! might be Power BI Report Server which you should know) and check properties. 
>![image](https://github.com/1015062E/howto/assets/160798406/6511e056-c2b2-4bfb-905f-b7f95d57abe1)
>![image](https://github.com/user-attachments/assets/b18e8cc0-765d-4f95-8555-9f2dfb75d906)


##### 4).Then you can find your Reporting Service installation location. e.g. : 
>![image](https://github.com/1015062E/howto/assets/160798406/ca74bdd6-9ad3-41a3-8fa4-21702e969c58)



#### 5).You could then find some folders within main installation folder, like below. 
>![image](https://github.com/1015062E/howto/assets/160798406/e7025842-eba9-464c-bb59-5206f53a0569)
>![image](https://github.com/user-attachments/assets/1529581f-7ad2-4fc1-be33-5b1748aa8030)


#### 6).To collect Reporting Service logs, please select and compress the whole LogFiles folder
Note : If you have multile instances joined in scale-out group, please do same operation for each instance. 
><br>![image](https://github.com/1015062E/howto/assets/160798406/83d31447-5a99-4caa-9b5a-6000737040a3)

