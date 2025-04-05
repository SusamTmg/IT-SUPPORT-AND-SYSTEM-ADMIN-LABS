**Week 1 – Windows Server, Active Directory, and Domain Configuration**

In Week 1 of my IT Support Self-Training Program, I simulated a real company IT environment using VMware.
This included setting up a Windows Server 2019 domain controller, configuring Active Directory, creating users/groups, applying GPOs, and simulating real-world IT support tasks such as password resets, RDP setup, and file sharing.

**Skills Practiced:**

VMware virtualization setup
Windows Server & Client installation
Active Directory Domain Services (AD DS)
Organizational Units (OUs), users, groups and User Management
DNS configuration for domain join
Group Policy (GPO) configuration and enforcement: Password policy, USB restriction, Control Panel block, Account lockout
Troubleshooting domain logins & DNS issues
Remote Desktop (RDP) setup and permissions
File sharing with NTFS permissions

**Real-World IT Tasks This Week Maps To:**

**Active Directory & GPO** are used daily by IT teams to manage users, secure access, and enforce company-wide policies.
**DNS misconfigurations**, **account lockouts**, and **domain login issues** are real support tickets in IT support environments.
**RDP and NTFS file sharing** reflect common tasks IT support handles during onboarding, system handovers, and issue resolution.


## Subtopics / Lab Files for WEEK 1

`01_vm-setup.md` – VMware setup, Server & Client installation  
`02_active-directory.md` – AD DS setup and domain controller configuration  
`03_user-group-setup.md` – Creating users, groups, and OUs  
`04_domain-login-troubleshooting.md` – Fixing domain login issues and DNS config  
`05_gpo-policies.md` – Enforcing password, USB, and Control Panel policies  
`06_lockout-events.md` – Simulating and troubleshooting account lockouts  
`07_rdp_ntfs-permissions.md` – Configuring RDP and secure file sharing  
`troubleshooting-log.md` – Notes on real issues faced & how they were resolved 

## What I Learned

- How companies use Windows Server to manage users, computers, and policies through Active Directory (AD)
- Why a Domain Controller is essential in a professional IT environment
- The role of DNS in domain login and how incorrect settings break authentication
- How Group Policy (GPO) is used to enforce company-wide security settings like password complexity, USB blocking, and lockout rules
- The difference between local and domain user accounts and how login formatting matters (e.g., TECHSOLUTIONS\john.smith)
- How to simulate and resolve real IT issues such as login failures, account lockouts, and remote desktop access problems
- How to use Event Viewer and audit policies to trace security events like failed logins (Event ID 4740)
- Why NTFS permissions and shared folder access are critical for secure file sharing across company networks
- How to build, configure, and troubleshoot a professional domain setup using only virtual machines and free tools

