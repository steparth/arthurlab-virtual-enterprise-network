File Services (SMB) Configuration
Overview

This section documents the deployment and configuration of SMB File Services within the ArthurLab Virtual Enterprise Network.

Three departmental network shares were created to simulate a small enterprise file server:

Share	Purpose
Public Shares	General file sharing for all users
IT Share	Operating system and application software
HR Share	Human Resources documents

The shares were created using Server Manager → File and Storage Services on SERVER01.

Step 1 – Open File and Storage Services

Open Server Manager.

Navigate to

Server Manager
    └── File and Storage Services
            └── Shares

Click Tasks → New Share.

Select

SMB Share – Quick

Click Next.

Expected Result

The New Share Wizard opens.


Step 2 – Create the IT Share

Enter the following information.

Field	Value
Share Name	IT Share
Local Path	C:\Shares\IT Share
Description	Application and Operating System Software

Click Next.

Expected Result

The wizard creates the shared folder and assigns the appropriate SMB path.

\\SERVER01\IT Share



Step 3 – Create the Public Share

Create another SMB share.

Field	Value
Share Name	Public Shares
Local Path	C:\Shares\Public Shares

Click Next.

Expected Result

The Public Shares folder is prepared for sharing.

Step 4 – Review Share Configuration

Review the SMB settings before creating the share.

The following settings were enabled.

Setting	Value
Protocol	SMB
Access-Based Enumeration	Enabled
Caching	Enabled
Encrypt Data	Enabled

Click Create.

Expected Result

The configuration summary is displayed.


Step 5 – Verify Share Creation

After clicking Create, verify that Windows reports the following.

Create SMB Share        Completed

Set SMB Permissions     Completed

This confirms that the network share was successfully created.


Step 6 – Configure Share Permissions

Open

Properties
Sharing
Advanced Sharing
Permissions

Assign permissions according to departmental requirements.

Example configuration.

User / Group	Permission
Everyone	Read
Stephen Admin	Full Control
Ophelia Sales	Change

This demonstrates role-based access control within the Active Directory environment.



Step 7 – Validate the Share

From a Windows client, press

Windows + R

Enter

\\server01.int.arthurlab.com\Public Shares

or

\\SERVER01\Public Shares

Verify that:
The share opens successfully.
Permissions are enforced according to the assigned user.
Users can access only the resources for which they have been granted permission.
Verification Checklist
Test	Expected Result	Status
SMB Share Wizard Opens	Successful	
IT Share Created	Successful	
Public Share Created	Successful	
SMB Permissions Assigned	Successful	
Share Accessible from Client	Successful	
Lessons Learned

This exercise demonstrated the deployment of centralized SMB file services within a Windows Server environment. Department-specific network shares were created using Server Manager, and role-based access permissions were configured to control user access. By enabling Access-Based Enumeration and SMB encryption, the file services were configured to provide a secure and organized shared storage environment suitable for enterprise use.
