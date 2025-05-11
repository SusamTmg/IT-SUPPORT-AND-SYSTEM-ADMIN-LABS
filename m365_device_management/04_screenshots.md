# Microsoft 365 User Security & Access Log

This document captures key screenshots from the learning of the Microsoft 365 Device Management simulation.The images focus on successful tasks such as user creation, multi-factor authentication (MFA) setup, and secure login.

While some Intune and device policies could not be fully tested due to environment limitations, these screenshots highlight the key workflows IT admins commonly perform when onboarding users and enforcing identity protection in Microsoft 365.

### **User Creation Summary – Emily Taylor**
This screenshot shows the final step of creating a Microsoft 365 cloud user (Emily Taylor) in the Admin Center. It includes all key configurations: the custom username, license assignment (Office 365 E5 – no Teams), region (Australia), and default role (no admin privileges).
This step is important in real IT support because creating cloud users with proper access, licensing, and regions is often part of onboarding workflows — especially in hybrid or remote companies.

![Image](https://github.com/user-attachments/assets/fc6f44b7-7362-44a8-ad51-3d6a672ddbd5)
---

### **Active Users Dashboard – Microsoft 365 Admin Center**
This screenshot displays the list of active cloud users created during the lab: Emily Taylor, Arjun Mehra, and Jisoo Park, along with the admin account Susam Study. Each user was added through the Microsoft 365 Admin Center and assigned an Office 365 E5 (no Teams) license.

These user accounts were used to simulate real employee identities for testing security configurations like MFA and login workflows. This dashboard allows IT admins to manage accounts, apply policies, and perform common support tasks such as resetting passwords or modifying access permissions in a real enterprise environment.

![Image](https://github.com/user-attachments/assets/b3bb1f50-0ffd-4333-8e15-46a923d2f9b1)
---

### **MFA & First-Time Login Simulation**
These screenshots document the real-world workflow of onboarding a new Microsoft 365 user with enforced multi-factor authentication (MFA).
We enabled legacy MFA for user Emily Taylor, and then logged in using her credentials to simulate a first-time sign-in:

MFA Enforcement: Emily was selected in the Microsoft Entra Admin Center and MFA was enabled using the legacy per-user method.

MFA Registration Prompt: Upon first login, Emily was required to set up Microsoft Authenticator before gaining access.

Password Update: As expected for newly created users, the system enforced a password change after MFA was configured.

![Image](https://github.com/user-attachments/assets/4345d93b-bb64-4f7f-9ed2-e35d185574d1)
![Image](https://github.com/user-attachments/assets/28c9e4a4-ab08-42e1-967c-149260e6e291)
![Image](https://github.com/user-attachments/assets/b515a10c-76e3-4018-97cd-90890ec5e47c)
---

### **Successful Microsoft 365 Login After MFA Setup**

This screenshot shows the successful login of the test user Emily Taylor after completing MFA registration and password reset. The user is now fully signed into the Microsoft 365 Copilot interface, confirming that account provisioning and security policies were applied correctly.

This simulates a real enterprise environment where users access productivity tools (Outlook, OneDrive, Teams) after identity verification and secure onboarding.

![Image](https://github.com/user-attachments/assets/3a313b07-2341-4695-827f-c0659e46894e)
---














