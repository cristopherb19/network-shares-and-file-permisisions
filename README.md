<p align="center">
<img src="https://i.imgur.com/L4QkhAs.png" alt="lab 7"/>
</p>

# Microsoft Azure Lab: Network File Shares and Permissions

## Overview
In this lab, we will work with Network File Shares and Permissions on Microsoft Azure to demonstrate an understanding of file share configurations and permissions. **We will be using the DC-1 and Client-1 virtual machines (VMs) from the previous Active Directory lab.**

### Prerequisites
1. Access to the DC-1 VM as a domain administrator account (`mydomain.com\jane_admin`).
2. Access to the Client-1 VM as a normal domain user (`mydomain\<someuser>`).
3. Previous setup of an Active Directory environment with DC-1 and Client-1.

---

## Lab Instructions

### Step 1: Create Sample File Shares with Various Permissions
1. **Log into DC-1** using the domain admin account `mydomain.com\jane_admin`.
2. On the `C:\` drive of DC-1, create the following four folders:
   - `read-access`
   - `write-access`
   - `no-access`
   - `accounting`

![image](https://github.com/user-attachments/assets/70f4cb60-c509-4f8d-9788-3bc6078194ba)

3. Set the following permissions for each folder:
   - **Folder:** `read-access`  
     **Group:** `Domain Users`  
     **Permission:** `Read`  
     *(Share the folder with these settings.)*

![image](https://github.com/user-attachments/assets/4045f78d-54ea-44df-9bf4-52c29cd03c48)

![image](https://github.com/user-attachments/assets/8152ebef-841b-464a-8a9b-5840b85e80a4)

![image](https://github.com/user-attachments/assets/d7727851-a695-49aa-9ad3-e1abca2923a7)

![image](https://github.com/user-attachments/assets/c7a2b05e-415d-4a6e-be41-047d6d7e8885)

![image](https://github.com/user-attachments/assets/e12e2f0d-78e5-46e0-8d21-e7345620b973)

   - **Folder:** `write-access`  
     **Group:** `Domain Users`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

![image](https://github.com/user-attachments/assets/1a4526c9-5257-4b03-8117-fb15b565c5cf)

   - **Folder:** `no-access`  
     **Group:** `Domain Admins`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

![image](https://github.com/user-attachments/assets/04e31115-aaaa-40d5-849a-6b7489f6b922)

   - **Folder:** `accounting`  
     *(Do not configure permissions yet; skip this for now.)*

---

### Step 2: Attempt to Access File Shares as a Normal User
1. **Log into Client-1** using a normal user account (`mydomain\<someuser>`).
2. Navigate to the shared folders:
   - Open file explorer.
   - Enter `\\dc-1` to access shared folders on DC-1.
3. Test access to the folders:
   - Which folders can you access? 
   - Which folders can you create files in?

![image](https://github.com/user-attachments/assets/d1ced96e-4c81-4551-9755-b38fe1cdb609)

![image](https://github.com/user-attachments/assets/eac4cc38-8519-49ce-b29c-2428514c0843)

![image](https://github.com/user-attachments/assets/ad87e709-492b-414f-b0eb-5731d9b617bf)

![image](https://github.com/user-attachments/assets/822c8faa-bf5d-45d5-bde1-3e6701075251)

---

### Step 3: Create an "ACCOUNTANTS" Security Group, Assign Permissions, and Test Access
1. **Log into DC-1** as the domain admin account (`mydomain.com\jane_admin`).
2. Open Active Directory and create a security group named `ACCOUNTANTS`.

![image](https://github.com/user-attachments/assets/26c7574d-fead-4c69-b2f4-368372301efc)

3. Set permissions for the `accounting` folder:
   - **Folder:** `accounting`  
     **Group:** `ACCOUNTANTS`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

![image](https://github.com/user-attachments/assets/6695bf2d-045f-402e-8490-45332304292b)

4. Test access as the normal user:
   - On Client-1, while logged in as `<qaki.hof>` (or other user), try to access the `accounting` share via `\\dc-1`.  
     - **Expected Result:** Access to the folder should fail.

![image](https://github.com/user-attachments/assets/411aed0b-03d6-4046-8e2b-5a9d61783b84)

5. Assign `<qaki.hof>` (or other user) to the `ACCOUNTANTS` group:
   - On DC-1, add `<qaki.hof>` (or other user) as a member of the `ACCOUNTANTS` security group.
   - **Sidenote:** You can add entire groups to other groups as well. If we wanted to give access to all of the domain users we would assign 'Domain Users' to the 'ACCOUNTANTS' group instead of qaki.hof. 

![image](https://github.com/user-attachments/assets/0935824a-4032-42ea-83d9-f9dd11171dcb)

![image](https://github.com/user-attachments/assets/abfed4d2-f759-40c1-8171-1df8e952814d)

6. Re-test access as `<qaki.hof>`:
   - **Log out of Client-1** and log back in as `<qaki.hof>`.
   - Try to access the `accounting` share via `\\dc-1`.
     - **Expected Result:** Access to the folder should now succeed.
![image](https://github.com/user-attachments/assets/2b41e545-d81f-4ec1-838d-680877c7bb86)
---

## Conclusion
By completing this lab, you will have demonstrated:
- Configuring file shares with varying permissions.
- Testing access to file shares from different user accounts.
- Managing Active Directory security groups and applying permissions effectively.
