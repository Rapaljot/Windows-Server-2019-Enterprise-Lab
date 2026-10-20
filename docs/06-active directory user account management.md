## Windows Server 2019 — Active Directory User Account Management

## 1. Overview

After creating the Organizational Unit structure in Active Directory Domain Services (AD DS), the next step was to create and manage user accounts.

In an enterprise environment, every employee typically receives a unique user account that allows them to authenticate to the organization's domain and access authorized resources.

Active Directory provides centralized user management, allowing administrators to create, modify, disable, and manage employee accounts from a central location.

For this lab, I simulated a small company with 15 employees distributed across four departments.

## Objectives

The objectives of this section are to:

1. Understand Active Directory user accounts.
2. Plan employee accounts and naming conventions.
3. Create user accounts in Active Directory.
4. Organize employees into departmental Organizational Units.
5. Configure account passwords.
6. Modify employee account properties.
7. Reset user passwords.
8. Disable and enable user accounts.
9. Unlock locked user accounts.
10. Verify user account configuration using PowerShell.

---

## Lab Environment

| Component               | Configuration                        |
| ----------------------- | ------------------------------------ |
| Virtualization Platform | VMware Workstation                   |
| Operating System        | Windows Server 2019                  |
| Domain Controller       | DC01                                 |
| Active Directory Domain | rapaljotlab.local                    |
| Management Tool         | Active Directory Users and Computers |
| Total Employees         | 15                                   |
| Departments             | HR, Finance, Sales, IT               |

---

# Step 1 — Understand Active Directory User Accounts

## 1.1 What Is an Active Directory User Account?

An Active Directory user account represents an individual user within a Windows domain environment.

Each account contains information such as:

* First name
* Last name
* Username
* User principal name (UPN)
* Password
* Department
* Job title
* Account status
* Security group memberships

These accounts allow users to authenticate against Active Directory and access resources according to their assigned permissions.

### Example

A Human Resources employee named Sarah Johnson may have the following account information:

| Property            | Value             |
| ------------------- | ----------------- |
| First Name          | Sarah             |
| Last Name           | Johnson           |
| Full Name           | Sarah Johnson     |
| Username            | sarah.johnson     |
| Domain              | rapaljotlab.local |
| Department          | HR                |
| Organizational Unit | HR                |

Sarah can use her domain account to sign in to a domain-joined computer.

Her sign-in name could be:

```text
sarah.johnson@rapaljotlab.local
```

Alternatively, she could use:

```text
RAPALJOTLAB\sarah.johnson
```

Both formats can identify her Active Directory domain account.

---

# Step 2 — Plan Employee User Accounts

Before creating accounts, I planned the employee structure.

A consistent naming convention helps administrators identify users and makes account management easier.

For this lab, I used the following username format:

```text
firstname.lastname
```

For example:

```text
sarah.johnson
```

This naming convention is easy to understand and commonly used in corporate environments.

## 2.1 Human Resources Department

| Employee       | Username       | Department |
| -------------- | -------------- | ---------- |
| Sarah Johnson  | sarah.johnson  | HR         |
| Emma Wilson    | emma.wilson    | HR         |
| Olivia Martin  | olivia.martin  | HR         |
| James Anderson | james.anderson | HR         |

## 2.2 Finance Department

| Employee      | Username      | Department |
| ------------- | ------------- | ---------- |
| Mike Brown    | mike.brown    | Finance    |
| Sophia Davis  | sophia.davis  | Finance    |
| Daniel Taylor | daniel.taylor | Finance    |
| Emily White   | emily.white   | Finance    |

## 2.3 Sales Department

| Employee      | Username      | Department |
| ------------- | ------------- | ---------- |
| David Smith   | david.smith   | Sales      |
| Michael Clark | michael.clark | Sales      |
| Jessica Moore | jessica.moore | Sales      |
| Ryan Walker   | ryan.walker   | Sales      |

## 2.4 Information Technology Department

| Employee      | Username      | Department |
| ------------- | ------------- | ---------- |
| Jennifer Lee  | jennifer.lee  | IT         |
| Robert Harris | robert.harris | IT         |
| Kevin Thomas  | kevin.thomas  | IT         |

### Total Employee Accounts

A total of 15 fictional employee accounts were planned.

All employees will be placed in the appropriate departmental Organizational Units.

---

# Step 3 — Open Active Directory Users and Computers

I used Active Directory Users and Computers (ADUC) to create and manage the employee accounts.

## 3.1 Configuration Steps

1. Started the Windows Server 2019 virtual machine.
2. Logged in using the domain Administrator account.
3. Opened **Server Manager**.
4. Clicked **Tools** in the upper-right corner.
5. Selected **Active Directory Users and Computers**.

The Active Directory management console opened.

### Alternative Method

The console can also be opened using the Run dialog.

Press:

`Windows + R`

Enter:

```cmd
dsa.msc
```

Press **Enter**.

![alt text](<../images/06-active directory user account management/01.png>)

*Figure 1: Opening Active Directory Users and Computers on DC01.*

---

# Step 4 — Navigate to the HR Organizational Unit

The first employee account was created in the Human Resources department.

## 4.1 Configuration Steps

1. Opened **Active Directory Users and Computers**.

2. Expanded the domain:

   `rapaljotlab.local`

3. Expanded the parent Organizational Unit:

   `RapaljotLab`

4. Expanded the `Users` Organizational Unit.

5. Selected the `HR` Organizational Unit.

The HR OU will contain employee accounts belonging to the Human Resources department.

### Organizational Unit Path

```text
rapaljotlab.local
│
└── RapaljotLab
    │
    └── Users
        │
        └── HR
```

![alt text](<../images/06-active directory user account management/02.png>)

*Figure 2: Navigating to the Human Resources Organizational Unit.*

---

# Step 5 — Create the First Active Directory User

The first user account created in this lab was for Sarah Johnson, an employee in the Human Resources department.

## 5.1 Open the New User Wizard

### Configuration Steps

1. Right-clicked the `HR` Organizational Unit.
2. Selected **New**.
3. Clicked **User**.

The **New Object — User** window appeared.

This wizard allows administrators to create a new user account in Active Directory.

## 5.2 Enter Employee Information

I entered the following information:

| Field           | Value             |
| --------------- | ----------------- |
| First Name      | Sarah             |
| Last Name       | Johnson           |
| Full Name       | Sarah Johnson     |
| User Logon Name | sarah.johnson     |
| Domain          | rapaljotlab.local |

The user logon name was configured as:

```text
sarah.johnson@rapaljotlab.local
```

I then clicked **Next**.

![alt text](<../images/06-active directory user account management/03.png>)

*Figure 3: Creating an Active Directory user account for Sarah Johnson.*

---

# Step 6 — Configure the User Account Password

After entering the employee information, I configured the account password.

Active Directory requires user accounts to follow the password policies configured for the domain.

These policies may define password length, complexity, password history, and other security requirements.

## 6.1 Configure the Initial Password

### Configuration Steps

1. Entered a temporary password in the **Password** field.

2. Re-entered the password in the **Confirm password** field.

3. Selected:

   **User must change password at next logon**

4. Left **User cannot change password** unchecked.

5. Left **Password never expires** unchecked.

6. Left **Account is disabled** unchecked.

7. Clicked **Next**.

### Why Require a Password Change?

Requiring a password change at the next logon ensures that the employee creates a new password after receiving the temporary credentials.

This is a useful security practice during employee onboarding.

> **Security Note:** Passwords must never be displayed in screenshots or stored in public GitHub documentation.

![alt text](<../images/06-active directory user account management/04.png>)

*Figure 4: Configuring password options for a new Active Directory user account.*

---

# Step 7 — Complete the User Creation Wizard

After configuring the password, the wizard displayed a summary of the user account settings.

## Configuration Steps

1. Reviewed the employee information.
2. Confirmed the username.
3. Confirmed the selected password options.
4. Clicked **Finish**.

The new user account was created in the HR Organizational Unit.

## Verification

I selected the HR OU and confirmed that the following user appeared:

`Sarah Johnson`

![alt text](<../images/06-active directory user account management/05.png>)

*Figure 5: Verifying that Sarah Johnson was created inside the HR Organizational Unit.*

---

# Step 8 — Create the Remaining HR Employees

After creating the first employee account, I repeated the same process for the remaining Human Resources employees.

## Employees Created

| Employee       | Username       |
| -------------- | -------------- |
| Sarah Johnson  | sarah.johnson  |
| Emma Wilson    | emma.wilson    |
| Olivia Martin  | olivia.martin  |
| James Anderson | james.anderson |

## Configuration Steps

For each employee:

1. Right-clicked the `HR` Organizational Unit.
2. Selected **New > User**.
3. Entered the employee's first and last name.
4. Configured the username.
5. Clicked **Next**.
6. Entered a temporary password.
7. Selected **User must change password at next logon**.
8. Clicked **Next**.
9. Reviewed the information.
10. Clicked **Finish**.

After creating the accounts, I verified that all four employees appeared inside the HR OU.

![alt text](<../images/06-active directory user account management/06.png>)

*Figure 6: Verifying the Human Resources employee accounts.*

---

# Step 9 — Create Finance Department Employees

Next, I created user accounts for employees in the Finance department.

## 9.1 Navigate to the Finance OU

In Active Directory Users and Computers, I navigated to:

```text
rapaljotlab.local
└── RapaljotLab
    └── Users
        └── Finance
```

## 9.2 Create Finance Accounts

I created the following employee accounts:

| Employee      | Username      |
| ------------- | ------------- |
| Mike Brown    | mike.brown    |
| Sophia Davis  | sophia.davis  |
| Daniel Taylor | daniel.taylor |
| Emily White   | emily.white   |

### Configuration Steps

1. Right-clicked the Finance OU.
2. Selected **New > User**.
3. Entered the employee information.
4. Configured the user logon name.
5. Entered a temporary password.
6. Selected **User must change password at next logon**.
7. Completed the wizard.
8. Repeated the process for the remaining Finance employees.

## Verification

I verified that all four accounts appeared inside the Finance OU.


![alt text](<../images/06-active directory user account management/07.png>)

*Figure 7: Verifying the Finance department employee accounts.*

---

# Step 10 — Create Sales Department Employees

After creating the Finance accounts, I created employee accounts for the Sales department.

## 10.1 Navigate to the Sales OU

```text
rapaljotlab.local
└── RapaljotLab
    └── Users
        └── Sales
```

## 10.2 Create Sales Accounts

| Employee      | Username      |
| ------------- | ------------- |
| David Smith   | david.smith   |
| Michael Clark | michael.clark |
| Jessica Moore | jessica.moore |
| Ryan Walker   | ryan.walker   |

### Configuration Steps

1. Opened the Sales Organizational Unit.
2. Right-clicked the OU.
3. Selected **New > User**.
4. Entered the employee details.
5. Configured the username and temporary password.
6. Selected the password-change requirement.
7. Completed the user creation wizard.
8. Repeated the process for all Sales employees.

## Verification

I confirmed that four employee accounts appeared inside the Sales Organizational Unit.

![alt text](<../images/06-active directory user account management/08.png>)

*Figure 8: Verifying the Sales department employee accounts.*

---

# Step 11 — Create IT Department Employees

The final department was Information Technology.

IT employees are responsible for supporting users, computers, networks, and other technology resources.

For this lab, I created three IT employee accounts.

## 11.1 Navigate to the IT OU

```text
rapaljotlab.local
└── RapaljotLab
    └── Users
        └── IT
```

## 11.2 Create IT Accounts

| Employee      | Username      |
| ------------- | ------------- |
| Jennifer Lee  | jennifer.lee  |
| Robert Harris | robert.harris |
| Kevin Thomas  | kevin.thomas  |

### Configuration Steps

1. Opened the IT Organizational Unit.
2. Right-clicked the OU.
3. Selected **New > User**.
4. Entered the employee's information.
5. Configured the user logon name.
6. Assigned a temporary password.
7. Required the user to change their password at the next logon.
8. Completed the wizard.
9. Repeated the process for the remaining IT employees.

### Important Security Consideration

Although these employees belong to the IT department, I did not automatically assign administrative privileges to their accounts.

Administrative privileges should only be granted when required for an employee's responsibilities.

This follows the principle of least privilege.

## Verification

I confirmed that three employee accounts appeared in the IT OU.

![alt text](<../images/06-active directory user account management/09.png>)

*Figure 9: Verifying the IT department employee accounts.*

---

# Step 12 — Configure Employee Account Properties

After creating the user accounts, I explored the user properties available in Active Directory.

These properties allow administrators to maintain important employee information.

## 12.1 Open User Properties

### Configuration Steps

1. Opened **Active Directory Users and Computers**.
2. Navigated to the HR OU.
3. Located `Sarah Johnson`.
4. Right-clicked the user account.
5. Selected **Properties**.

The user account Properties window opened.

This window contains several tabs used to configure account information.

---

## 12.2 Configure Employee Information

I reviewed the available employee information fields.

These included:

* General
* Address
* Account
* Profile
* Telephones
* Organization
* Member Of

For this exercise, I selected the **Organization** tab.

I entered the following example information:

| Property   | Value           |
| ---------- | --------------- |
| Job Title  | HR Coordinator  |
| Department | Human Resources |
| Company    | RapaljotLab     |

After entering the information, I clicked **Apply** and then **OK**.

![alt text](<../images/06-active directory user account management/10.png>)

*Figure 10: Configuring employee information in Active Directory user properties.*

---

# Step 13 — Reset a User Password

Password resets are among the most common tasks performed by IT Help Desk Technicians.

Employees may forget their passwords or need new passwords when they cannot access their accounts.

For this lab, I practiced resetting a password for a fictional employee.

## 13.1 Open the Password Reset Dialog

### Configuration Steps

1. Opened **Active Directory Users and Computers**.
2. Navigated to the HR OU.
3. Located `Sarah Johnson`.
4. Right-clicked the account.
5. Selected **Reset Password**.

The Reset Password window appeared.

## 13.2 Assign a New Temporary Password

1. Entered a new temporary password.
2. Confirmed the password.
3. Selected **User must change password at next logon**.
4. Clicked **OK**.

Windows displayed a confirmation message if the password reset was successful.

![alt text](<../images/06-active directory user account management/11.png>)

*Figure 11: Resetting an employee's Active Directory password.*

### Result

The password reset operation completed successfully.

The employee can use the temporary password at the next sign-in and will be prompted to create a new password.

---

# Step 14 — Disable an Active Directory User Account

Disabling user accounts is another common administrative task.

When an employee leaves a company, their account may need to be disabled to prevent further authentication.

For this lab, I practiced disabling a fictional employee account.

## 14.1 Configuration Steps

1. Opened **Active Directory Users and Computers**.

2. Navigated to the Sales OU.

3. Located the account:

   `ryan.walker`

4. Right-clicked the user account.

5. Selected **Disable Account**.

6. Confirmed the operation.

The account was disabled.

### Explanation

A disabled account cannot be used for new domain sign-ins.

However, disabling an account does not automatically terminate every existing session or revoke all previously issued access tokens.

![alt text](<../images/06-active directory user account management/12.png>)

*Figure 12: Disabling an Active Directory user account.*

---

# Step 15 — Enable a Disabled User Account

After testing the account disabling process, I re-enabled the employee account.

## 15.1 Configuration Steps

1. Opened **Active Directory Users and Computers**.
2. Navigated to the Sales OU.
3. Located `Ryan Walker`.
4. Right-clicked the disabled account.
5. Selected **Enable Account**.
6. Confirmed the operation.

The account was enabled again.

![alt text](<../images/06-active directory user account management/13.png>)

*Figure 13: Re-enabling a disabled Active Directory user account.*

### Result

The user account was enabled successfully and was available for authentication, subject to the account's other settings and permissions.

---

# Step 16 — Understand and Manage Account Lockouts

Active Directory can lock user accounts when incorrect passwords are entered repeatedly, depending on the configured account lockout policy.

Account lockouts help protect against repeated unauthorized sign-in attempts.

## 16.1 Understanding Account Lockouts

An account may become locked when the number of failed sign-in attempts reaches the threshold configured in the domain's account lockout policy.

For example, if a domain policy specifies an account lockout threshold, repeated incorrect passwords can trigger a lockout.

> **Note:** The default lockout policy may not lock accounts automatically. A lockout threshold must be configured for this behavior.

## 16.2 Unlock a User Account

If an account is locked, it can be unlocked through Active Directory Users and Computers.

### Configuration Steps

1. Opened **Active Directory Users and Computers**.
2. Located the affected user.
3. Right-clicked the user account.
4. Selected **Properties**.
5. Opened the **Account** tab.
6. Located the account unlock option, if the account was locked.
7. Selected **Unlock account**.
8. Clicked **Apply** and **OK**.

Alternatively, the account can be unlocked from the Reset Password dialog when the unlock option is available.

![alt text](<../images/06-active directory user account management/14.png>)

*Figure 14: Reviewing the account unlock option for a locked Active Directory user.*
### Result

After unlocking the account, the employee could attempt to sign in again using valid credentials.

---

# Step 17 — Verify Employee Accounts Using PowerShell

After creating the employee accounts, I used Windows PowerShell to verify their configuration.

PowerShell provides command-line tools for querying and managing Active Directory objects.

## 17.1 Open PowerShell

1. Opened the Start menu.
2. Searched for **Windows PowerShell**.
3. Opened PowerShell.
4. Imported the Active Directory module:

```powershell
Import-Module ActiveDirectory
```

---

## 17.2 Display All Active Directory Users

I executed:

```powershell
Get-ADUser -Filter *
```

### Explanation

The `Get-ADUser` cmdlet retrieves user account information from Active Directory.

The `-Filter *` parameter retrieves all user accounts in the search scope.

The output includes built-in accounts as well as the employee accounts created for the lab.

---

## 17.3 Display Usernames and Account Status

To display a more organized output, I executed:

```powershell
Get-ADUser -Filter * -Properties Enabled |
    Select-Object Name, SamAccountName, Enabled
```

### Explanation

This command displays:

* Full name
* Username
* Account status

The `Enabled` property indicates whether the user account is enabled.

![alt text](<../images/06-active directory user account management/15.png>)

*Figure 15: Verifying Active Directory user accounts using PowerShell.*

---

# Step 18 — Verify Users in Each Department

After verifying the user accounts, I checked that employees were placed in the correct Organizational Units.

For example, to display all users in the HR OU, I executed:

```powershell
Get-ADUser -Filter * `
    -SearchBase "OU=HR,OU=Users,OU=RapaljotLab,DC=rapaljotlab,DC=local" |
    Select-Object Name, SamAccountName
```

### Explanation

The `-SearchBase` parameter limits the search to a specific Active Directory location.

This command retrieves the user accounts stored inside the HR Organizational Unit.

I repeated the verification for the Finance, Sales, and IT departments by changing the OU name in the distinguished name.

![alt text](<../images/06-active directory user account management/16.png>)

*Figure 16: Verifying employee accounts within departmental Organizational Units using PowerShell.*

---

# Step 19 — Verify the Total Number of Employees

After creating all employee accounts, I verified the total number of users inside the company's Organizational Unit.

I executed:

```powershell
Get-ADUser -Filter * `
    -SearchBase "OU=Users,OU=RapaljotLab,DC=rapaljotlab,DC=local" |
    Measure-Object
```

### Expected Output

```text
Count : 15
```

### Explanation

The `Measure-Object` cmdlet counts the number of objects returned by the previous command.

Because the Users OU contains the departmental OUs, the search retrieves employee accounts from the nested Organizational Units.

![alt text](<../images/06-active directory user account management/17.png>)

*Figure 17: Verifying the total number of employee accounts in Active Directory.*

---

# Step 20 — Final Verification

After completing the account creation and management tasks, I reviewed the Active Directory user configuration.

## Employee Distribution

| Department | Expected Users |
| ---------- | -------------: |
| HR         |              4 |
| Finance    |              4 |
| Sales      |              4 |
| IT         |              3 |
| **Total**  |         **15** |

## Verification Checklist

| Task                          | Expected Result |
| ----------------------------- | --------------- |
| Create HR Accounts            | 4 accounts      |
| Create Finance Accounts       | 4 accounts      |
| Create Sales Accounts         | 4 accounts      |
| Create IT Accounts            | 3 accounts      |
| Configure User Properties     | Successful      |
| Reset User Password           | Successful      |
| Disable User Account          | Successful      |
| Enable User Account           | Successful      |
| Review Account Unlock Process | Completed       |
| Verify Users Using PowerShell | Successful      |
| Verify Employee Count         | 15 users        |

---

# Conclusion

In this section, I practiced Active Directory user account management using Windows Server 2019.

I created a fictional company environment containing 15 employee accounts distributed across Human Resources, Finance, Sales, and Information Technology.

Each employee account was created inside the appropriate departmental Organizational Unit.

I also practiced common IT administration tasks, including:

* Creating Active Directory users
* Configuring temporary passwords
* Requiring password changes
* Managing user properties
* Resetting employee passwords
* Disabling user accounts
* Enabling user accounts
* Reviewing account lockouts
* Verifying accounts using PowerShell

These exercises provided hands-on experience with common Active Directory administration tasks performed by IT Help Desk Technicians and System Administrators.

## Next Phase

The next phase of the lab will focus on creating and managing **Active Directory Security Groups**.

I will create department-based groups, add employees to their appropriate groups, and explore the AGDLP model for managing access permissions.

---
