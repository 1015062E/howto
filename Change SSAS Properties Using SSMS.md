<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

To change properties in SQL Server Analysis Services (SSAS) using SQL Server Management Studio (SSMS), follow these steps:

1. **Open SSMS**: Launch SQL Server Management Studio and connect to your SSAS instance.
2. **Connect to SSAS**: In the Object Explorer, right-click on the SSAS server instance and select **Properties**.
3. **Access Properties**: In the Properties window, ensure you check the **Show Advanced (All) Properties** checkbox to display all available properties.
4. **Locate the Property**: Scroll through the list to find the property you want to change. For example, `ExternalCommandTimeout`.
5. **Set the Value**: Change the value of the selected property to your desired setting. For instance, set `ExternalCommandTimeout` to `10800` (which is equivalent to 3 hours).
6. **Apply Changes**: Click **OK** to apply the changes.
7. To make the changes take effect, you need to **restart the SSAS instance**. 

<br>[General properties](https://learn.microsoft.com/en-us/analysis-services/server-properties/general-properties?view=asallproducts-allversions)
