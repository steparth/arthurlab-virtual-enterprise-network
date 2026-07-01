Group Policy and Security Implementation


Overview

This section documents the implementation of Group Policy Objects (GPOs) used to manage workstation security and user configurations within the ArthurLab Active Directory environment.

The following policies were implemented:

Account Lockout Policy
Desktop Restrictions
Organizational Unit (OU) GPO Linking
Group Policy Refresh
Policy Validation
Step 1 – Create a New Group Policy Object

A dedicated Group Policy Object was created for workstation management instead of modifying the Default Domain Policy.

Procedure
Open Group Policy Management.
Expand Forest → Domains → int.arthurlab.com.
Right-click the target Organizational Unit (IT).
Select Create a GPO in this domain, and Link it here.
Name the policy:
ArthurLab System Management Group Policy Object
Expected Result

A new GPO is linked to the IT Organizational Unit.


Step 2 – Configure Desktop Restrictions

The newly created GPO was edited to apply workstation policies.

Procedure
Right-click the new GPO.
Select Edit.
Navigate to:
User Configuration
    └── Policies
        └── Administrative Templates
            └── Desktop
Enable:
Hide and disable all items on the desktop
Expected Result

Users within the IT Organizational Unit cannot access desktop icons.



Step 3 – Configure Account Lockout Threshold

To improve security, an account lockout policy was implemented.

Navigate to:

Computer Configuration

    Policies

        Windows Settings

            Security Settings

                Account Policies

                    Account Lockout Policy

Configure:

Setting	Value
Account Lockout Threshold	3 Invalid Logon Attempts
Expected Result

After three failed logon attempts, the user account is locked.



Step 4 – Verify Account Lockout Policy
After configuring the threshold, verify the policy settings.

The following values should be displayed:

Setting	Value
Account Lockout Duration	10 minutes
Account Lockout Threshold	3 invalid logon attempts
Reset Counter After	5 minutes


Step 5 – Apply the Updated Policies
After modifying the Group Policy Objects, force an update.
Run the following command from an elevated Command Prompt:
gpupdate /force

Expected Output:

Updating policy...

Computer Policy update has completed successfully.

User Policy update has completed successfully.

This confirms that the updated Group Policy settings have been applied successfully.

Step 6 – Validate Account Lockout
To verify the effectiveness of the account lockout policy:
Attempt to log in using an incorrect password.
Repeat until the configured threshold is reached.
Windows should prevent further logon attempts.

The client displays:

"The referenced account is currently locked out and may not be logged on to."

This confirms that the policy is functioning as intended.
4.5 – Successful Account Lockout Validation
Verification Summary
Configuration	Status
New GPO Created	
Desktop Restrictions Applied	
Account Lockout Threshold Configured	
Group Policy Updated	
Account Lockout Successfully Tested	

Lessons Learned
Implementing Group Policy Objects (GPOs) provided centralized management of workstation security across the Active Directory domain. By separating workstation policies into a dedicated GPO linked to the appropriate Organizational Unit, administrative tasks became more organized and easier to manage. Testing confirmed that security settings were successfully propagated to client computers through gpupdate /force, and the account lockout policy effectively protected the environment against repeated failed authentication attempts. This exercise demonstrated the importance of structured Group Policy design and validation in a Windows enterprise environment.
