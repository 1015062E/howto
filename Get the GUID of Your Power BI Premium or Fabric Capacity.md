### Step-by-Step Guide to Find the GUID in the Power BI Admin Portal

Here’s how you can retrieve the GUID for your Power BI Premium or Fabric capacity:

1. **Sign In to Power BI Service**  
   Open your browser and log in to the Power BI Service using your admin credentials.

2. **Access the Settings Menu**  
   In the top-right corner of the Power BI interface, locate and click the **Settings (⚙️)** icon.

3. **Navigate to the [Admin Portal](https://app.powerbi.com/admin-portal)**  
   From the dropdown menu, select **Admin Portal** to access the administrative controls.

4. **Go to Capacity Settings**  
   In the left-hand menu of the Admin Portal, find and click on **Capacity settings**. This section lists all capacities associated with your tenant.

5. **Select Your Capacity**  
   Identify and click on the specific **Premium capacity** or **Fabric capacity** you’re working with. This opens the capacity’s details page.

6. **Locate the GUID in the URL**  
   Once on the capacity details page, check the browser’s address bar. The URL will follow this structure:  https://app.powerbi.com/admin-portal/capacities/GUID?experience=power-bi, The `<GUID>` portion—typically a string of letters and numbers (e.g., `123e4567-e89b-12d3-a456-426614174000`)—is the unique identifier you need. Copy this value for your records.
