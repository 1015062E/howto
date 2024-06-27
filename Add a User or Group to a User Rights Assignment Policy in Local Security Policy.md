## Prerequisites

Before you begin, you need to have the following:

- A Windows computer with administrative privileges
- A user or group account that you want to add to a user rights assignment policy
- A user rights assignment policy that you want to modify

## Steps

To add a user or group to a user rights assignment policy in Local Security Policy, follow these steps:

1. Press `Win + R` keys to open Run, type `secpol.msc` into Run, and click OK to open Local Security Policy.
2. Expand `Local Policies` in the left pane of Local Security Policy, and click on `User Rights Assignment`.
3. In the right pane of User Rights Assignment, double click on the policy you want to add users and/or groups to.
4. Click on the `Add User or Group` button.
5. Click on the `Object Types` button.
6. Check all the boxes for Object types, and click OK.
7. Click on the `Advanced` button.
8. Click on the `Find Now` button, select the name of the user or group you want to add, and click OK.
9. Click OK again to close the dialog box and apply the changes.
10. Restart the application/windows service before making further tests. 
