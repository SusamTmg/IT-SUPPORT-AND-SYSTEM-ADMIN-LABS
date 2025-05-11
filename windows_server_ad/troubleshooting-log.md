# Troubleshooting Log

This log documents all the technical issues encountered in this IT Support Self-Training Program and the step-by-step solutions applied. All scenarios were replicated in a virtual lab setup using Windows Server 2019 and Windows 10 client.

---

## 1. Client Not Joining Domain

**Issue:** Client machine failed to join the domain (remained in WORKGROUP).  
**Cause:** DNS was not set to point to the Domain Controller.  
**Fix:** Set the DNS on the client machine to the IP address of the Windows Server (192.168.192.129). Confirmed domain resolution using `nslookup techsolutions.local`.

---

## 2. Domain User Login Failed

**Issue:** Login failed for domain users on the Windows 10 Client.  
**Cause:** Used local login format instead of domain login format.  
**Fix:** Used correct domain login format: `TECHSOLUTIONS\john.smith` or `john.smith@techsolutions.local`. The system prompted for a password reset, confirming successful domain authentication.

---

## 3. Group Policy (GPO) Not Applying

**Issue:** GPO changes were not taking effect on the client machine.  
**Cause:** The Windows Server (Domain Controller) was offline.  
**Fix:** Turned on the Domain Controller and ran `gpupdate /force` on the client to force policy updates. GPOs then applied successfully.

---

## 4. Account Not Locking After Failed Logins

**Issue:** Entering incorrect passwords multiple times didn’t lock the domain user account.  
**Cause:** Client was not receiving the lockout policy due to server being off.  
**Fix:** Ensured the Domain Controller was on, then ran `gpupdate /force` again. Retested login attempts — account locked as expected after 5 failed logins.

---

## 5. “Account is Locked Out” Not Showing in ADUC

**Issue:** Could not see that the user was locked in Active Directory Users and Computers (ADUC).  
**Fix:** Refreshed ADUC after confirming server was online. Verified that the “Unlock account” option was available for `john.smith`.

---

## 6. Event Viewer Log (Event ID 4740) Missing

**Issue:** Account lockout events were not being recorded in Event Viewer.  
**Cause:** Account logon audit policies were not enabled.  
**Fix:** Enabled auditing using Local Security Policy and verified audit settings using the command: `auditpol /get /category:*`. Once enabled, Event ID 4740 logs appeared under Security.

---

## 7. Control Panel Access Still Restricted

**Issue:** Even after disabling the GPO for Control Panel restriction, the client could not access it.  
**Cause:** GPO was still linked at the domain level or hadn’t updated.  
**Fix:** Unlinked the GPO from the domain level using Group Policy Management Console (GPMC), and ran `gpupdate /force` on the client. Access to Control Panel and Settings was restored.

---

## 8. Cannot Run CMD as Administrator on Client

**Issue:** User was unable to open Command Prompt as Administrator.  
**Cause:** The user account (john.smith) was a standard domain user without admin privileges.  
**Fix:** Switched to a local administrator account or used domain administrator credentials to elevate privileges where needed.

---

## 9. Remote Desktop (RDP) Login Failed

**Issue:** Domain user `john.smith` could not connect to the client via Remote Desktop (mstsc).  
**Cause:** User was not a member of the Remote Desktop Users group, and RDP policy wasn’t applied.  
**Fix:**  
- Added `TECHSOLUTIONS\john.smith` to the Remote Desktop Users group on the client  
- Configured “Allow log on through Remote Desktop Services” in GPO under User Rights Assignment  
- Applied changes with `gpupdate /force` and successfully tested RDP login from the server

---

## 10. Shared Folder Access Denied

**Issue:** `john.smith` couldn’t access the shared folder hosted on the Windows Server.  
**Cause:** Either NTFS permissions or Share permissions were not configured properly.  
**Fix:**  
- Configured NTFS permissions: Gave Modify access to `john.smith`  
- Set Share permissions to allow Full Control  
- Tested access using `\\192.168.192.129\Shared_Folder` → Verified user could read/write files

---

## Summary

- **DNS is foundational:** All domain-related services rely on correct DNS pointing to the Domain Controller.  
- **GPOs:** Require the Domain Controller to be online and either `gpupdate /force` or wait for auto-application.  
- **Audit policies:** Must be manually enabled to log critical security events like account lockouts.  
- **Permissions:** RDP access, shared folders, and elevated actions require correct group memberships and policies.  
- **Real-world readiness:** Each issue was solved using professional tools like ADUC, GPMC, Event Viewer, auditpol, and system troubleshooting — mirroring real job scenarios in corporate IT support environments.
