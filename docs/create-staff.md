# Create a Staff User

## Overview

When a new staff member joins The Seattle School, a user profile must be created for this person. First, the user is added to Active Directory. From there, a Google Sync is run to create a Google account for the user and set them up with access to email. Finally, alias and delegate email access is added for the users that need it.

## Create Active Directory User Account

1. Get connected to the Domain Controller server **SHALOM (10.15.1.19)**. A connection can be established through ConnectWise Automate ScreenConnect or Remote Desktop Connection.

2. Log into the server as the Domain Admin account **g3t0n1t**. The credentials can be found in PassPortal.

    *Note: Although any domain admin account will authenticate, g3t0n1t is used for this process because the user profile contains some necessary files.*

3. From the Start menu, launch **Active Directory Administrative Center**.

4. In the lefthand pane, select the root directory **areopagos (local)**.

5. Navigate to **Managed\Google\Users\Staff-Faculty**. All Staff user accounts reside within this directory.

6. Locate the appropriate subdirectory based on the user being provisioned.

    *If you are not sure which category the user falls into, reach out to Kartha at kheinz@theseattleschool.edu for clarification.*

    * **FolderRedirect** is the most common folder. It is for all users who utilize our workstations. Many staff members are assigned a laptop when they begin work, and these users will reside within FolderRedirect.

    * **Local Users** are users who utilize our shared-use workstations on-site. This encompasses two groups of staff members: **PL** and **RLP**.

        * **PL** is for Practicum Leaders. These are Assistant Instructors and part-time faculty members.
    
        * **RLP** is for Resilient Leaders Project. This project is now known as the Center for Transforming Engagement (CTE), and all CTE employees should be in this group.

    * **Offsite** are users who only work outside of the building. These are likely to be contractors who don't work with a set regular schedule like part-time or full-time employees.

        * **Adjunct** are adjunct faculty members. These faculty teach remotely and are contracted for a term.

        * **Board** are Board of Directors members. This list seldom changes.

        * **RFPT** are instructors for the RFPT certificate.

        * **TheAllenderCenter** are TAC certificate instructors. This is not the group for all TAC employees; rather, it is just the contracted instructors who lead group sessions during certificate training weekends.

    * **TOJ** are The Other Journal employees. TOJ is a publication we partner with.

7. From within the appropriate subdirectory, select New > User.

8. Fill in the following information for the user:
    * First Name
    * Last Name
    * User UPN logon
        * Username format: `[first initial][last name]` e.g. dmcneil
        * Choose theseattleschool.edu from the dropdown
    * Password & Confirm Password
        * This should be set to the Initial temporary password for newly created staff AD accounts (not student accounts) found in PassPortal
    * Email Address
        * This will look similar to the User UPN logon field. e.g. dmcneil@theseattleschool.edu
        * This field is used for ADFS to connect to the user account to validate for apps i.e. Populi
    * Department
        * i.e. IT, HR, Admissions, etc.
        * This field is used to sync to KnowBe4 security training
    * Member Of
        * This is determined by **MASTER_Staff_Provisioning**
        * All users should be a member of Domain Users
        * Google Drive Folder Edit Access is controlled by group objects beginning with role-
        * Institutional Calendar access is controlled by group objects beginning with role-calendar-
        * Dynamics users need to be added to DynamicBudgetUsers group
        * Mail groups fall into four categories: Administrative Staff, Instructional Staff, Student Employee, and Allender Center Instructor
            * There are further classifications within each mail group category, but some users just receive the parent group.
            * Each of these groups is a member of AllStaff
        * The group object for access to each network share for each department is listed in **MASTER_Staff_Provisioning** at the very top, e.g. AcademicsStaff for Academics department
        * Click the Add... button, type each object name, then click Check Names to find each appropriate group, then click OK

9. Click OK to create the user.

## Create Google User Account

The Google Workspace directory is controlled by Active Directory. After making changes to the AD environment, the changes must be synced to Google Workspace by running a Google Cloud Directory Sync.

1. Ensure that you are still signed onto SHALOM as g3t0n1t.

2. Ensure that a Network drive is mapped to **N:** from **\\axio\departments**. If not, map the drive with the following command in Command Prompt: `net use N: \\axio\departments`

3. From the Start menu, expand the **Google Cloud Directory Sync** folder and launch **Configuration Manager**.

4. From the menu bar, select *File > Open Recent...* and locate *N:\IT\Scripts\Active\Google\theseattleschool.edu-shalom.xml*.

5. From the lefthand pane, click Sync.

6. Check the box labeled **Clear cache**, then click **Simulate sync**. Wait for this process to finish and verify that the changes appear accurate.

7. When you are ready to make the changes, close the simulation window and click **Sync & Apply Changes**. When asked to confirm, click **Yes**. Wait for the process to complete and verify again that the changes appear accurate.

## Alias and Delegate Email Access

Refer to **MASTER_Staff_Provisioning** to determine if the new employee should have an email alias, or delegate access to an email account. If the user should have delegate email access, [refer to this document](/tss-it-sop/delegate-mailbox). If the user should have an email alias, follow these steps.

*At the time of writing this document, the only email alias available is @theallendercenter.org. A new email alias will be available soon for @theotherjournal.com.*

1. Log in to a Google Admin account at **admin.google.com**.

2. Under Directory, click Users. Search for the user and click on their name.

3. On the left side, click the **Add alternate emails** section.

4. Fill in the following information:

    * Alternate email: [the same username as their main email]
    * Domain: [theallendercenter.org]

5. Click **Save**.

## Next Steps

Once all these steps are finished, the user accounts are all ready and the next step is to [provide access for applications](/tss-it-sop/applications-staff).