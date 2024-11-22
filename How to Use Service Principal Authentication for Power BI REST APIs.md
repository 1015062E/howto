# <Deprecated!!! Stop referring to this post>

<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

# How to Use Service Principal Authentication for Power BI REST APIs

## Steps

Here are the steps to use service principal authentication for Power BI REST APIs:

1. Create an Azure AD app: You can create an Azure AD app in the Azure portal by signing in, searching for and selecting "App registrations", and then selecting "New registration". Fill in the required information and select "Register". After you register your app, the Application ID is available from the Overview tab. Copy and save the Application ID for later use.
2. Create an Azure AD security group: You can create a new Security Group in Azure Active Directory. Make sure to select "Security" as the Group type.
3. Add your App-Id as a member of the security group: Navigate to Azure portal > Azure Active Directory > Groups, and choose the security group you created in Step 2. Select "Add Members" and add your App-Id as a member of the security group.
4. Enable the Power BI service admin setting: Log in to the Power BI admin portal. You need to be a Power BI admin to see the tenant settings page. Under "Admin API settings", you'll see "Allow service principals to use read-only Power BI admin APIs". Set the toggle to "Enabled", and then select the "Specific security groups" radio button and add the security group you created in Step 2 in the text field that appears below it.
5. Grant access to Power BI workspaces: To use the Power BI REST APIs, you also need to grant access to the service principal to the workspaces that contain the resources you want to access. To do this:
    1) Log in to the Power BI portal and navigate to the workspace where you want to grant access.
    2) Select the workspace and then click on the "Access" tab.
    3) Click the "Add user" button and enter the email address or name of the security group you created in Step 2.
    4) Select the access level you want to grant (i.e., viewer, contributor, member or admin). Grant admin access if you need the service principal to invoke Power BI REST API like refreshing a dataflow or dataset.
    5) Click "Add" to save the changes.

It might take a few minutes for these changes to take effect. Especially if you have granted admin role to the security group that the service principal belongs to but still receive a 403 error code when invoking an API call. In this case, please wait for some time (half - one hour) and try again.

## You may find below screenshots helpful when doing above tasks. 

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/ea9d76b4-f00a-48b2-947e-173829991e04)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/f3f65ea4-38ad-464c-901c-807ed5a10ada)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/41e3c90f-4c4d-40e5-aff3-0910cb0da8c1)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/d46bd1ac-96d3-44d4-bbc7-9edc2215b262)

// Select those items as needed, refer to Power BI REST API doc(https://learn.microsoft.com/en-us/rest/api/power-bi/) to see which permission you need to add according to what you want the service principal to do. 

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/7263f935-dca1-4c93-964a-4e98b4660b73)

// In case the 'admin consent required' is marked as 'Yes' but the 'Status' shows it's not approved, do : 
<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/4972dca0-427a-415c-abbd-314b8112dc1b)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/019a95bd-af17-4eee-ac62-341e518cd982)

<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/643fc2a8-22a8-456f-8973-df3ff0ee8186)

## Documentation References

For more information on using service principal authentication for Power BI REST APIs, you can refer to these official documents:

- [Embed Power BI content with service principal and an application secret](https://learn.microsoft.com/en-us/power-bi/developer/embedded/embed-service-principal)
- [Enable service principal authentication for read-only admin APIs](https://learn.microsoft.com/en-us/power-bi/enterprise/read-only-apis-service-principal-authentication)
- [Power BI REST APIs](https://learn.microsoft.com/en-us/rest/api/power-bi/)
