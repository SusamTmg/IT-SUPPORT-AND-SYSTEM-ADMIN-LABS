## 01_Microsoft_365_MFA_User_Onboarding

This document outlines the process I followed to enforce Multi-Factor Authentication (MFA) for a Microsoft 365 user account using the legacy per-user method, simulate a real user's first login, and test successful MFA registration and password reset.

---

##  Objective

To simulate the onboarding process for a new employee who is required to register for MFA and change their temporary password during first login. This is a common Tier 1 IT support task in modern cloud-based organizations.

---

##  Users Involved

| Display Name | Username | Role |
|--------------|----------|------|
| Emily Taylor | EmilyTaylor@TechCloud888.onmicrosoft.com | Test end-user |
| Susam Study (me) | Admin/Global Admin | Administrator (MFA enforcer) |

---

##  Steps Performed

### 1. Enabled MFA for Emily (per-user method)
- Logged into [https://admin.microsoft.com](https://admin.microsoft.com)
- Navigated to: **Users > Active Users > Multi-Factor Authentication**
- Searched for Emily Taylor and set MFA to **Enabled**
- Confirmed that user status changed to **Enforced** after login attempt

---

### 2. Simulated first login as Emily
- Opened **incognito window** in Edge
- Visited: [https://portal.office.com](https://portal.office.com)
- Entered: `EmilyTaylor@TechCloud888.onmicrosoft.com`
- Entered temporary password set during user creation
- Was immediately prompted to:
  - Register MFA (via Microsoft Authenticator QR code)
  - Set a new permanent password

---

### 3. Completed MFA registration
- Used **Microsoft Authenticator app**
- Opened app > Added “Work or School Account” > Scanned QR code
- Successfully approved test push notification

---

### 4. Verified MFA + password reset
- Logged in again to confirm new password + MFA works
- Accessed Microsoft 365 dashboard as Emily
- Visited [https://mysignins.microsoft.com](https://mysignins.microsoft.com) to confirm MFA was active 

---

##  What I Learned

- MFA enforcement is a **critical first step** in securing Microsoft 365 user accounts.
- Legacy per-user MFA is still widely used in many orgs, especially for small businesses.
- Real IT teams must guide users through this process, especially for first-time login issues or MFA device changes.
- Tools like `mysignins.microsoft.com` allow users and admins to verify sign-in history, reset authentication methods, and troubleshoot login issues.

---

##  Notes

This process was fully completed and verified using Microsoft 365 Admin Center and an incognito session to simulate a real end-user experience. This task reflects typical responsibilities of Tier 1 and Tier 2 IT support staff handling identity security in hybrid or cloud-first environments.
