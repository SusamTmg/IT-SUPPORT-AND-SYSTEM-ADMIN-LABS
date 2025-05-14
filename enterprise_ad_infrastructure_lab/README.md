#  Enterprise Active Directory Infrastructure Lab

This lab simulates a real-world **multi-site Active Directory environment** with multiple Domain Controllers (DCs), password replication policies, and secure group-based access control.

It includes the use of **Install From Media (IFM)** for efficient DC promotion, a **Read-Only Domain Controller (RODC)** for remote office security, and end-to-end **login testing** for validation — all managed within a Windows Server-based identity infrastructure.

---

##  What I Practiced

- Promoting a second Domain Controller (PLABDM01) using **Install From Media (IFM)**
- Creating a **Read-Only Domain Controller (PLABSA01)** using PowerShell
- Setting up **Password Replication Policies** and caching for remote login
- Managing **Active Directory Users and Groups**
- Creating and applying **VPN Users** group for role-based access
- Performing **login tests** from a Windows 10 client to confirm domain-wide replication

---

##  Why This Lab Matters in Real IT Jobs

> This lab replicates tasks done in **enterprise IT environments** where identity, access, and security need to scale across multiple office locations.

I built a full enterprise domain structure with:
-  Multiple DCs to support failover and replication
-  RODC for safe, limited AD access in remote branches
-  Configurable login policies and access groups
-  Hands-on PowerShell use for admin-level tasks

These are daily tasks for System Administrators, Infrastructure Engineers, and IT Support roles in companies with hybrid or distributed teams.

---

## 🛠 Tools & Technologies

| Category                 | Tools / Concepts Used                               |
|--------------------------|-----------------------------------------------------|
| AD Setup & Promotion     | `ntdsutil`, `Install-ADDSDomainController`, IFM     |
| Password Replication     | RODC, PRP, Allowed RODC Password Replication Group  |
| Role-Based Access        | VPN Users group, ADUC, security group management    |
| Testing & Verification   | Domain logins, credential caching, ADUC validation  |
| PowerShell & CLI         | Credential input, role verification, IP config      |

---

##  File Structure

| File/Folder         | Description |
|---------------------|-------------|
| `commands/`         | PowerShell and AD promotion commands used |
| `lab_summary/`      |Full breakdown of the lab steps with screenshots and explanations |

---

##  Workflow Summary

1. Configured PLABDC01 as the primary Domain Controller  
2. Created IFM media using `ntdsutil`  
3. Mapped drive to PLABDM01 and promoted it using IFM  
4. Promoted PLABSA01 as a Read-Only Domain Controller using PowerShell  
5. Configured Password Replication Policy for specific users  
6. Created “VPN Users” group and assigned users for simulated role-based access  
7. Logged in from PLABWIN10 using a domain account to verify setup

---

## What I Learned

- How to design and configure a **multi-DC AD environment**  
- How to use **IFM** to improve performance and reduce replication traffic  
- The purpose and use of a **Read-Only DC (RODC)** in real-world companies  
- How to control password caching and improve remote login reliability  
- How to simulate **real company access control** using AD groups

---


## This lab reflects my ability to:

- Build **enterprise-level Active Directory infrastructure**
- Manage **identity, access, and security** across multiple systems
- Use **PowerShell**, GUI tools, and configuration files to deploy, control, and verify AD services
- Understand **replication**, **branch office design**, and **user access policies**

This project was built to deepen my skills in **Windows Server**, **identity management**, and **IT support environments**.
