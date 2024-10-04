If you have a list of Azure AD User Object IDs and need to find the corresponding usernames and other contact information, follow the steps below. This guide provides two methods to retrieve user details using the Azure Portal and the Microsoft 365 Admin Center.

## Method 1: Using Azure Portal

1. **Login to Azure Portal**:
   - Go to Azure Portal https://aka.ms/azureportal
   - Sign in with your credentials.

2. **Navigate to Microsoft Entra ID**:
   - In the left-hand navigation pane, select **Microsoft Entra ID**. <br>![image](https://github.com/user-attachments/assets/c8ce9af4-6abf-4971-ad64-d19ef6aad864)
   - Then click on **Manage** | **Users** | **All Users** <br>![image](https://github.com/user-attachments/assets/ce03f49e-4116-4298-aabf-3f294a1672bf)

3. **Search for User**:
   - Use the search bar to enter the User Object ID.<br>![image](https://github.com/user-attachments/assets/01688e0f-048e-4157-b3e3-8b8fbc938778)
   - The corresponding user details, including the username, will be displayed.

## Method 2: Using Microsoft 365 Admin Center

1. **Go to Microsoft 365 Admin Center**:
   - Open your browser and go to Microsoft 365 Admin Center https://admin.microsoft.com/Adminportal/Home#/users
   - Sign in with your admin credentials.

2. **Export User List**:
   - In the left-hand navigation pane, select **Users**.
   - Click on **Active users**.
   - Select **Export Users** to download a list of all users.<br>![image](https://github.com/user-attachments/assets/cb95c010-e78d-4fdc-8cc1-022a575d8ef3)

3. **Check Object ID and Contact Info**:
   - Open the exported file in Excel or any spreadsheet application.
   - Search for the User Object ID to find the corresponding username and other contact information.
