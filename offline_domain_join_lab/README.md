#  Offline Domain Join Lab (Windows Server & Active Directory)

This lab demonstrates how to join a Windows 10 client to a Windows Server Active Directory domain using **Offline Domain Join (ODJ)** — a real-world enterprise technique used when client machines cannot directly connect to the Domain Controller during deployment.

It also includes **user account auditing**, **account lockout policy testing**, and **login rights configuration**, simulating the kind of identity management work performed by IT support and system administrators.

---

##  What I Practiced

- Using `djoin.exe` to provision a computer account and join it to the domain offline
- Copying domain metadata from the server to a remote client machine
- Importing the metadata and rebooting the client to finalize the domain join
- Enforcing security rules like **account lockout after failed login attempts**
- Using PowerShell to find **locked**, **disabled**, and **inactive** user accounts
- Granting and restricting **local and remote login permissions** through User Rights Assignment

---

##  Why This Matters in Real IT Jobs

> This lab is based on **exact tasks that real IT professionals do daily**, especially when supporting users in different offices or working remotely.

Companies use **Offline Domain Join** to:
- Pre-configure laptops for remote staff
- Deploy devices in low-connectivity environments
- Enforce centralized security policies through Active Directory

I have simulated those tasks here, showing my ability to work with:
- Windows Server
- PowerShell scripting
- Domain controller infrastructure
- Security policy enforcement

---

##  Tools & Skills Demonstrated

| Area                     | Tools & Concepts Used                            |
|--------------------------|--------------------------------------------------|
| Domain Join              | `djoin.exe`, Active Directory Users & Computers |
| Account Auditing         | `Search-ADAccount` in PowerShell                |
| Security Policies        | Local Security Policy (User Rights Assignment)  |
| Troubleshooting & Setup  | CLI tools, command sequencing, reboot handling  |

---

## File Structure

| File/Folder            | Description |
|------------------------|-------------|
| `lab_summary.md`       | Full breakdown of the lab steps with screenshots and explanations |
| `commands/`            | PowerShell and CMD commands used during the lab |

---

## What I Learned

- How to join machines to a domain **without direct server access**
- How to enforce and test **password lockout policies**
- How to use PowerShell for **user account management**
- How to set **login permissions** securely for different user roles

---

## This lab reflects my ability to:

- Understand and apply **real-world system administration tasks**
- Work with **Active Directory**, **PowerShell**, and **Windows Server**
- Simulate **enterprise-level identity and access management**
- Follow **structured IT workflows** and explain them clearly


