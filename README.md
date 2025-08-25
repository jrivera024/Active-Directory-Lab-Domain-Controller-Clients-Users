# Active-Directory-Lab-Domain-Controller-Clients-Users

This lab builds on the previous setup by:
  - Promoting a VM as a Domain Controller.
  - Creating OUs, admin accounts, and employees.
  - Joining a client VM to the domain.
  - Setting up Remote Desktop for domain users.
  - Automating user creation with PowerShell.

## Part 1: Setup Domain Controller & Join Client
1. Install Active Directory on DC-1
  - Log into DC-1 as labuser.
  - Install Active Directory Domain Services (ADDS) role.
  - Promote server as a Domain Controller with a new forest:
  - Domain name: mydomain.com

    <img width="756" height="554" alt="image" src="https://github.com/user-attachments/assets/ef0c6456-45a6-4e8c-9799-f5e6b061feab" />

  - Restart DC-1 and log in as:
    - mydomain.com\labuser

2. Create Domain Admin Account
  - Open Active Directory Users and Computers (ADUC).
  - Create OUs:
    - _EMPLOYEES
    - _ADMINS

      <img width="294" height="512" alt="image" src="https://github.com/user-attachments/assets/208b75e8-84c7-403c-bc3a-a79ae393f5c4" />

  - Create new user:
     - Name: Jane Doe
     - Username: jane_admin
     - Password: Cyberlab123!
  - Add jane_admin to Domain Admins group.

    <img width="401" height="309" alt="image" src="https://github.com/user-attachments/assets/e1f1ed6a-c90d-4771-8f94-cdf68133f902" />

  - Log out and back in as:
    - mydomain.com\jane_admin


3. Join Client-1 to Domain
  - Ensure Client-1 DNS is set to DC-1’s private IP (already done).
  - Restart Client-1 from Azure Portal.
  - Log into Client-1 as local admin (labuser).
  - Join computer to mydomain.com (requires restart).

    <img width="324" height="406" alt="image" src="https://github.com/user-attachments/assets/178411df-abe0-4205-87ef-d8adc96961ad" />

  - On DC-1, open ADUC → verify Client-1 appears under Computers.

    <img width="751" height="301" alt="image" src="https://github.com/user-attachments/assets/ac32df2a-dea6-4424-83b4-2396f9324e2e" />

  - Create new OU _CLIENTS and move Client-1 into it.

    <img width="485" height="304" alt="image" src="https://github.com/user-attachments/assets/45cd9b0b-473e-4c78-8546-ea522047d181" />
---

## Part 2: Remote Desktop & Bulk User Creation

4. Enable RDP for Domain Users
  - Turn on DC-1 and Client-1 in Azure Portal.
  - Log into Client-1 as mydomain.com\jane_admin.
  - Open System Properties → Remote Desktop.
  - Allow Domain Users access.
    -  Now, normal users can RDP into Client-1.

      <img width="378" height="329" alt="image" src="https://github.com/user-attachments/assets/1d5c6e87-7a2d-4d68-934b-8dd2d79b4c51" />

5. Bulk Create Users with PowerShell
  - On DC-1, log in as jane_admin.
  - Open PowerShell ISE as Administrator.
  - Paste the following script into a new file:

    ![image](https://github.com/user-attachments/assets/5f72befa-a87c-41db-bc5a-22372c2a516d)

  - Run the script → accounts will be created under _EMPLOYEES OU.

    <img width="947" height="300" alt="image" src="https://github.com/user-attachments/assets/aaf06458-f0d4-41fe-b3c4-e23b244ff1a2" />

  - Open ADUC to verify new users exist.

    <img width="746" height="526" alt="image" src="https://github.com/user-attachments/assets/6688a8c1-6e25-48b4-bc10-02e5d5a996fa" />

  - Attempt to log into Client-1 with one of the new users:
    - Example: mydomain.com\bax.beq
    - Password: Password1

      <img width="801" height="627" alt="image" src="https://github.com/user-attachments/assets/dd6ad13f-b9e9-4835-9c21-7369c532d98c" />

6. 
