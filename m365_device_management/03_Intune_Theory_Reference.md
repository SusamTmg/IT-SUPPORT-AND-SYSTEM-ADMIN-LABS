# 03 – Microsoft Intune: Theory & Enterprise Use Cases

This file summarizes key Microsoft Intune concepts that are essential for modern IT support and device management. While I couldn’t test every feature hands-on due to tenant restrictions, I studied how each component works in enterprise environments and documented real-world use cases.

---

##  What is Microsoft Intune?

**Microsoft Intune** is a cloud-based endpoint management platform that allows organizations to manage devices, apps, and user access securely — without needing physical access **or VPN connectivity**.

Admins can use Intune to:
- Enforce security rules (e.g., require passwords, block USBs)
- Push software (e.g., install Teams or Zoom remotely)
- Wipe lost/stolen devices
- Control what apps are allowed or restricted

---

##  Key Components of Intune

### 1. **Device Enrollment**

Enrollment is how a device joins the organization's system so that Intune can manage it.

Common enrollment methods:
- **Azure AD Join**: Used for corporate-owned devices (e.g., laptops for new employees)
- **BYOD (Bring Your Own Device)**: Personal devices register via Microsoft Authenticator or Company Portal app
- **Windows Autopilot**: For mass deployment — laptops arrive pre-configured and auto-enroll on first boot

---

### 2. **Compliance Policies**

These define whether a device is considered “healthy” and allowed to access corporate resources.

**Examples**:
- Is antivirus enabled?
- Is the disk encrypted with BitLocker?
- Is the OS up to date?

Used with Conditional Access to block non-compliant devices.

---

### 3. **Configuration Profiles**

These are used to **push settings and restrictions** to managed devices.

**Examples**:
- Disable USB storage
- Enforce password complexity
- Set idle screen lock timeout
- Preconfigure Wi-Fi or VPN settings

---

### 4. **App Deployment**

Intune supports app deployment for:
- Microsoft Store apps
- Win32 (.exe) apps
- Office 365
- Internal or custom LOB apps

Admins can assign apps to users or devices and track installation status.

---

### 5. **Endpoint Security**

Advanced device protection settings, often used by security teams.

Includes:
- Defender for Endpoint policies
- Attack Surface Reduction (ASR)
- Firewall settings
- Encryption enforcement

---

##  Summary Table

| Feature | Purpose | Example |
|---------|---------|---------|
| **Enrollment** | Connect device to tenant (Azure AD Join) | Join new hire laptop via company login |
| **Compliance Policy** | Check if device meets security standards | Require antivirus + encryption |
| **Configuration Profile** | Enforce device settings | Disable USB, force screen lock |
| **App Deployment** | Install approved apps remotely | Push Zoom or PowerShell |
| **Endpoint Security** | Harden devices against threats | Apply Defender policy, block macros |

---

##  Why I Couldn’t Test This

My Microsoft 365 E5 developer tenant did not include:

- The **Mobility (MDM and MAM)** blade required to configure MDM auto-enrollment
- Access to **Intune compliance or configuration profiles**
- Full **device onboarding capabilities**

Attempts to create policies or join a VM resulted in **404 blade errors** or **missing service plan** messages.

---

##  What I Learned

- Microsoft Intune is the industry-standard MDM solution used by companies to manage devices securely from the cloud
- Each component (compliance, config, enrollment, security) plays a role in managing risk
- Even without testing everything hands-on, I now understand how to architect, document, and troubleshoot core Intune tasks
