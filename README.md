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

<img src="https://imgur.com/a6lTmOS.png" alt="lab 7"/>

3. Set the following permissions for each folder:
   - **Folder:** `read-access`  
     **Group:** `Domain Users`  
     **Permission:** `Read`  
     *(Share the folder with these settings.)*

<img src="https://imgur.com/OpYfKyd.png" alt="lab 7"/>

<img src="https://imgur.com/64VG5lg.png" alt="lab 7"/>

<img src="https://imgur.com/XzEL4uO.png" alt="lab 7"/>

<img src="https://imgur.com/flzuY9H.png" alt="lab 7"/>

<img src="https://imgur.com/r1Pik4C.png" alt="lab 7"/>

   - **Folder:** `write-access`  
     **Group:** `Domain Users`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

<img src="https://imgur.com/j9uZ22v.png" alt="lab 7"/>

   - **Folder:** `no-access`  
     **Group:** `Domain Admins`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

<img src="https://imgur.com/cP3aqHW.png" alt="lab 7"/>

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

<img src="https://imgur.com/9TX5JQS.png" alt="lab 7"/>

<img src="https://imgur.com/eyjUoXs.png" alt="lab 7"/>

<img src="https://imgur.com/XxHdogw.png" alt="lab 7"/>

---

### Step 3: Create an "ACCOUNTANTS" Security Group, Assign Permissions, and Test Access
1. **Log into DC-1** as the domain admin account (`mydomain.com\jane_admin`).
2. Open Active Directory and create a security group named `ACCOUNTANTS`.

<img src="https://imgur.com/PEmPLUS.png" alt="lab 7"/>

<img src="https://imgur.com/2d4kloM.png" alt="lab 7"/>

<img src="https://imgur.com/MZSXXOb.png" alt="lab 7"/>

<img src="https://imgur.com/SfI3Tcq.png" alt="lab 7"/>

3. Set permissions for the `accounting` folder:
   - **Folder:** `accounting`  
     **Group:** `ACCOUNTANTS`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

<img src="https://imgur.com/pbs7yYM.png" alt="lab 7"/>

4. Test access as the normal user:
   - On Client-1, while logged in as `<qaki.hof>` (or other user), try to access the `accounting` share via `\\dc-1`.  
     - **Expected Result:** Access to the folder should fail.

<img src="https://imgur.com/AapVtsS.png" alt="lab 7"/>

5. Assign `<qaki.hof>` (or other user) to the `ACCOUNTANTS` group:
   - On DC-1, add `<qaki.hof>` (or other user) as a member of the `ACCOUNTANTS` security group.
   - **Sidenote:** You can add entire groups to other groups as well. If we wanted to give access to all of the domain users we would assign 'Domain Users' to the 'ACCOUNTANTS' group instead of qaki.hof. 

<img src="https://imgur.com/oofmO3G" alt="lab 7"/>


6. Re-test access as `<qaki.hof>`:
   - **Log out of Client-1** and log back in as `<qaki.hof>`.
   - Try to access the `accounting` share via `\\dc-1`.
     - **Expected Result:** Access to the folder should now succeed.
<img src="https://imgur.com/dxrhBJi.png" alt="lab 7"/>
---

## Conclusion
By completing this lab, you will have demonstrated:
- Configuring file shares with varying permissions.
- Testing access to file shares from different user accounts.
- Managing Active Directory security groups and applying permissions effectively.
