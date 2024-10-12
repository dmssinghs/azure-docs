# Step 1: Open the subscription
Follow these steps:
1. Sign in to the Azure portal.
2. In the Search box at the top, search for subscriptions.
3. Click the subscription you want to use.
   The following shows an example subscription.
![image](https://github.com/user-attachments/assets/24e7ffea-0bf5-416f-a982-7c7382ab1566)

# Step 2: Open the Add role assignment page
Access control (IAM) is the page that you typically use to assign roles to grant access to Azure resources. It's also known as identity and access management (IAM) and appears in several locations in the Azure portal.
1. Click Access control (IAM).
   The following shows an example of the Access control (IAM) page for a subscription.
![image](https://github.com/user-attachments/assets/279172a2-d034-4e1b-8eca-32e76cb35caf)

2. Click the Role assignments tab to view the role assignments at this scope.
3. Click Add > Add role assignment. 
If you don't have permissions to assign roles, the Add role assignment option will be disabled.
![image](https://github.com/user-attachments/assets/0f1b1da0-ecd8-4f09-ad07-6a68de86602a)
The Add role assignment page opens.
# Step 3: Select the Owner role
The Owner role grant full access to manage all resources, including the ability to assign roles in Azure RBAC. You should have a maximum of 3 subscription owners to reduce the potential for breach by a compromised owner.
1. On the Role tab, select the Reader roles tab.
![alt text](image.png)
2. Select the Reader role.
3. Click Next.
4. Click Next.
# Step 4: Select who needs access
1. To select who needs access, follow these steps:
On the Members tab, select User, group, or service principal to assign the selected role to one or more Microsoft Entra users, groups, or service principals (applications).
![alt text](image-1.png)
2. Click Select members.
3. Find and select the users, groups, or service principals.
You can type in the Select box to search the directory for display name or email address.
![alt text](image-2.png)
4. Click Select to add the user to the Members list.
5. Click Select members.
# Step 5: Assign role
Follow these steps:
1. On the Review + assign tab, review the role assignment settings.
![alt text](image-3.png)
2. Click Review + assign to assign the role.