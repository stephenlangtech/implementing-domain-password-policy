# Security Policies Using Group Policy in Active Directory

In this tutorial, we configure password security policies using Group Policy in an Active Directory environment. The policies establish password expiration, complexity, and minimum password length requirements for domain users. This lab uses VMware Workstation with one Domain Controller and two Windows client virtual machines to demonstrate how Group Policy can centrally enforce password security requirements across a domain.

## Environments and Technologies Used

* VMware Workstation
* Windows Server
* Active Directory Domain Services (AD DS)
* Group Policy Management
* Group Policy Objects (GPOs)
* Windows Security Settings
* Windows Command Line

## Operating Systems Used

* Windows Server
* Windows 10

## Actions and Observations

### 1. Open Group Policy Management

* Open **Group Policy Management** on the Domain Controller.
* Expand the domain.
* Right-click **Default Domain Policy**.
* Select:
  **Edit**  
  
  <img src="https://example.com/image.png" width="80" height="80">

### 2. Navigate to Password Policy Settings

* Navigate to:

  **Computer Configuration**
  → **Policies**
  → **Windows Settings**
  → **Security Settings**
  → **Account Policies**
  → **Password Policy**

The Password Policy section contains the settings used to establish password requirements for domain accounts.

### 3. Configure Maximum Password Age

* Locate:
  **Maximum password age**
* Right-click the policy and select:
  **Properties**
* Change the value to:
  **60 days**
* Click:
  **Apply**
* Click:
  **OK**

This requires domain users to change their passwords after the configured 60-day period.

### 4. Enable Password Complexity Requirements

* Locate:
  **Password must meet complexity requirements**
* Right-click the policy and select:
  **Properties**
* Select:
  **Enabled**
* Click:
  **Apply**
* Click:
  **OK**

This requires domain passwords to meet Windows password complexity requirements.

### 5. Configure Minimum Password Length

* Locate:
  **Minimum password length**
* Right-click the policy and select:
  **Properties**
* Set the minimum password length to:
  **12 characters**
* Click:
  **Apply**
* Click:
  **OK**

This prevents users from creating passwords shorter than 12 characters.

### 6. Force a Group Policy Update

* Group Policy may take some time to automatically apply.
* To immediately request a Group Policy refresh, open **Command Prompt** on the client VM and run:

```cmd
gpupdate /force
```

* This forces the client to retrieve and process the latest applicable Group Policy settings.

### 7. Verify the Password Security Policy

* Log in to one of the domain-joined client VMs using a domain user account.
* Attempt to change the user's password.
* Test a password shorter than **12 characters** to verify that it is rejected.
* Test a password that does not meet the required complexity requirements.
* Verify that the configured password policies are being enforced on the client VM.

The policy can also be tested on the second domain-joined client VM to verify that the settings are centrally enforced across the domain.

## Results

The **Default Domain Policy** was successfully configured to enforce stronger password security requirements across the Active Directory domain. Domain users are required to use passwords that are at least **12 characters long**, meet Windows complexity requirements, and expire after **60 days**.

This demonstrates how Active Directory and Group Policy can be used to centrally enforce password security standards across multiple domain-joined workstations rather than manually configuring password requirements on individual computers.
