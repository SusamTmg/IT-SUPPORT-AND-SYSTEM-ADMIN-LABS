# Week 3 – Microsoft 365 Device Management & Intune Simulation

This lab focused on simulating enterprise Microsoft 365 identity and endpoint management using Microsoft Entra ID (formerly Azure AD), Intune, and virtual machines. The objective was to understand how organizations secure devices, enforce compliance, and manage users through cloud-based tools.

While my Microsoft 365 developer tenant lacked full Intune permissions, I completed core identity and security workflows and documented the expected device management procedures based on real-world enterprise use.

---

##  Skills Demonstrated

- Created and licensed Microsoft 365 user accounts
- Enforced and tested Multi-Factor Authentication (MFA) policies
- Simulated first-time login flow with MFA registration and password reset
- Navigated the Microsoft Entra Admin Center and user/device settings
- Attempted device onboarding via Azure AD Join
- Reviewed structure and use of compliance and configuration policies in Intune

---

##  Tasks Completed

| Task | Outcome |
|------|---------|
| Created users (Emily, Arjun, Jisoo) | DONE |
| Assigned Microsoft 365 E5 licenses | DONE |
| Enabled MFA (legacy method) for user | DONE |
| Simulated login and MFA registration | DONE |
| Explored Entra Admin Center & roles | DONE |
| Accessed Intune portal & reviewed policy options | DONE |
| Attempted Azure AD Join for VM |  Not successful (license limitation) |
| Tried to create Intune compliance/config profiles |  Blocked by restricted access |

---

##  What I Learned

- **Microsoft Intune** enables secure, remote management of Windows devices in enterprise networks.
- **Compliance policies** check if a device meets corporate standards (e.g., BitLocker, antivirus).
- **Configuration profiles** are used to enforce settings like USB restrictions or password complexity.
- **Azure AD Join** connects company laptops to the cloud for centralized identity and device control.
- **Licensing diagnostics** is a critical skill — understanding why a feature fails is part of real IT support.

---

## Environment Limitations (and Real-World Insight)
Due to Microsoft’s 2024 policy changes, my Microsoft 365 E5 developer tenant did not include full Intune MDM access:

- Device enrollment via Azure AD Join was blocked  
- “Mobility (MDM and MAM)” settings failed to load (blade error)  
- Compliance and configuration profile creation was restricted  

These limitations reflect real-world issues faced by IT admins when working with improperly licensed or misconfigured tenants. I documented each scenario with screenshots, expected outcomes, and workaround plans.

Compliance and configuration profile creation was restricted 
---
##  Linked Lab Documents
- 01_mfa_user_setup.md – MFA enforcement + simulation
- 02_device_enrollment_attempt.md – Attempted Intune onboarding
- 03_sops.md – SOPs for user creation, MFA reset, and onboarding
- 04_intune_theory_reference.md – Technical summary of Intune architecture
