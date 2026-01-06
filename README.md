 # Active Directory Domain Administration Lab

## 🔹 Objective of Project
To design and implement a **centralized domain environment** using Windows Server that enables:
- Central user authentication
- Role-based access control (RBAC)
- Secure file sharing
- Policy enforcement using Group Policy
- Monitoring and troubleshooting using server tools

---

## 🔹 Environment Used

| Component | Details |
|---------|--------|
| Hypervisor | Oracle VirtualBox |
| Server OS | Windows Server 2022 |
| Client OS | Windows 11 |
| Domain Name | lab.local |
| Domain Controller | DC01 |
| Network Type | Internal / NAT |
| Tools Used | Server Manager, ADUC, GPMC, Event Viewer |

---

## 🔹 Step-by-Step Implementation

### 1️⃣ Active Directory Domain Services (AD DS)
- Installed AD DS role using Server Manager
- Promoted server to Domain Controller
- Created new domain: `lab.local`
- Verified AD DS and DNS services

Domain Controller created successfully

---

### 2️⃣ Organizational Unit (OU) Structure
Created the following OUs inside `lab.local`:
- HR
- IT
- Workstations
- Users

 Logical organization of users and computers

---

### 3️⃣ User Management
Created domain users:

| Username | Department |
|--------|-----------|
| sheela | HR |
| athul vnair | IT |

- Users created in correct OUs
- Password policy enforced
- Domain login tested from Windows 11

 Successful domain authentication

---

### 4️⃣ Security Groups (RBAC)
Created security groups:

| Group Name | Purpose |
|-----------|--------|
| HR_Group | HR department access |
| IT_Group | IT department access |

- Users added to respective groups
- Permissions assigned via groups (RBAC)

 Permissions via Groups, not individual users

---

### 5️⃣ Domain Join (Windows 11)
- Configured client DNS to point to DC01
- Joined Windows 11 to `lab.local`
- Verified computer object in Active Directory

Client successfully joined domain

---

### 6️⃣ File Server & Shared Folders
Created shared folders:

| Folder | Purpose |
|-------|--------|
| HR_Share | HR-only access |
| IT_Share | IT-only access |

**Permissions Applied:**
- Removed default Users access
- Assigned NTFS permissions via security groups
- HR_Group → HR_Share
- IT_Group → IT_Share
Access verified from client systems

---

### 7️⃣ Group Policy Objects (GPO)
Configured GPO for HR users:

**Policies Applied:**
- Disabled Command Prompt
- Restricted user system access
 GPO linked to HR OU  
  Policy applied successfully

---

### 8️⃣ GPO Verification & Troubleshooting
Commands used:
gpupdate/force
gpresult/r

- Verified correct GPO application
- Confirmed IT users were unaffected

Policy enforcement successful

---

### 9️⃣ Event Viewer Monitoring
Reviewed logs:
- Application Logs
- System Logs
- Security Logs

Common events observed:
- Event ID 7023 – Service Control Manager
- Event ID 10016 – DistributedCOM warnings

 Identified critical vs informational events

---

## 🔹 Troubleshooting Performed

| Issue | Resolution |
|-----|-----------|
| Password policy error | Used strong password |
| Access denied | Corrected NTFS permissions |
| GPO not applying | Verified OU and GPO link |
| Service error | Checked service dependencies |
| Login issue | Verified DNS configuration |

---

## 🔹 Validation & Testing
- Domain login tested
-  File access verified
- GPO enforcement confirmed
- Group-based access validated
- Logs monitored using Event Viewer

---

## 🔹 Security Best Practices Followed
- Used Security Groups instead of individual users
- Implemented least privilege access
- Centralized authentication via Active Directory
- Policy-based restrictions using GPO
- Continuous monitoring via Event Viewer

---

## 🔹 Skills Demonstrated
- Windows Server Administration
- Active Directory Management
- Group Policy Management
- File Server & NTFS Permissions
- User & Group Management
- Troubleshooting & Monitoring
- Enterprise IT Best Practices

## 🔹 Challenges Faced During the Project
VM Network Connectivity (NAT vs Host-Only)
Initially, the Windows 11 client was unable to communicate with the Windows Server Domain Controller while using NAT networking in VirtualBox. As a result, domain join and server connectivity did not work as expected.
Resolution:
Identified that NAT does not reliably allow VM-to-VM communication
Changed the network adapter to Host-Only Adapter for both Server and Windows 11
Verified connectivity using ping and DNS resolution
Successfully joined Windows 11 to the domain and confirmed communication with the server
Learning Outcome:
Gained a clear understanding of VirtualBox networking modes
Learned when to use NAT vs Host-Only in enterprise lab environments
Improved troubleshooting skills for network-related issues in virtual setups
