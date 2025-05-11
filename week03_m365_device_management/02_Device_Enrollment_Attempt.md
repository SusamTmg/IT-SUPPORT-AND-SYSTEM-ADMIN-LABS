# 02 – Device Enrollment Attempt (Windows VM to Azure AD / Intune)

This document outlines my attempt to join a Windows 10 virtual machine (VM) to my Microsoft 365 tenant using Azure AD Join, with the goal of enrolling the device into Microsoft Intune for remote management and policy enforcement.

While the steps were followed correctly, the enrollment failed due to Microsoft licensing restrictions. This document explains what I attempted, what errors occurred, and what I would have done if full access was available.

---

##  Objective

To simulate a real-world scenario where a company laptop is joined to Microsoft Entra ID (Azure AD) and automatically enrolled into Intune, allowing IT to manage the device remotely.

This is a standard task for IT admins during new employee onboarding or when issuing corporate devices.

---

##  Steps Attempted

### 1. Prepared the Windows 10 VM
- Confirmed it was running **Windows 10 Pro**
- Confirmed internet access and time settings
- Logged in using a local admin account (`TECHSOLUTIONS\Administrator`)

### 2. Tried to join the device to Microsoft 365 tenant
- Went to: `Settings → Accounts → Access work or school → Connect`
- Entered: `EmilyTaylor@TechCloud888.onmicrosoft.com`
- Entered password and continued

### 3. Received error
- Message:  
   *“We couldn’t auto-discover a management endpoint matching the entered user ID.”*
- This means the system couldn’t locate the correct Mobile Device Management (MDM) authority (Intune)

---

## 🚧 What Went Wrong (Root Cause)

| Issue | Explanation |
|-------|-------------|
|  No MDM authority | My Microsoft 365 E5 developer tenant does not have the **Mobility (MDM and MAM)** blade active, which is required for auto-enrollment |
|  Missing Intune licensing | Attempts to access Intune enrollment menu (`EnrollmentMenu`) returned **404 error** |
|  No access to config/compliance profiles | Attempted to create policies but was blocked due to missing service plan permissions |

This is likely due to Microsoft’s 2024 policy update, which **limits Intune MDM features** even for tenants on 30-day trials with valid payment methods.


---

## What I Would Have Done (If It Worked)

If the tenant had full Intune access, I would have:

1. **Enabled MDM auto-enrollment** in the Tenant Admin Center  
   (`Mobility (MDM and MAM)` → Microsoft Intune → Scope: All Users)

2. **Completed Azure AD Join** from the VM  
   - Device would be enrolled into Intune  
   - Emily’s login would be tied to the device

3. **Created and assigned:**
   - **Compliance policy** (require antivirus, BitLocker)
   - **Configuration profile** (disable USB, enforce password rules)

4. **Confirmed device appears in Intune Devices dashboard**  
   - Monitored policy enforcement  
   - Collected screenshots for each step

---

##  What I Learned

- Intune and device onboarding rely heavily on **proper licensing**
- Microsoft 365 “E5” label doesn’t guarantee access to all features
- Understanding how to troubleshoot licensing issues is part of real IT support
- Azure AD Join and Intune auto-enrollment are standard onboarding steps in cloud-first companies
- Even when tools are blocked, being able to **simulate the process and document limitations professionally** still reflects job-ready thinking

---

##  Conclusion

While I could not complete the full enrollment process due to service plan restrictions, I followed the exact enterprise process, identified the root causes of failure, and explained what I would do in a licensed environment. This lab gave me confidence in troubleshooting cloud identity, device setup, and policy management workflows.
