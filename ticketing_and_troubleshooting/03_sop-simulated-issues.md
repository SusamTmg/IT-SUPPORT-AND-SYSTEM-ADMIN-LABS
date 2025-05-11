# 03 – SOPs for Simulated IT Issues

This document contains three Standard Operating Procedures (SOPs) created in this Lab's Portfolio. Each SOP outlines a clear, structured method for resolving common IT issues based on simulated tickets in Jira Service Management.

These reflect the support tasks I practiced and demonstrate how I would approach these issues in a professional IT environment.

---

## SOP 1: Clearing Stuck Print Jobs in Windows

**Purpose**  
Resolve issues where print jobs are stuck in the queue due to a frozen or corrupted print spooler service.

**Tools & Access Required**  
- Local or remote access to user’s device  
- Administrator rights  
- Familiarity with Windows Services and File Explorer

**When to Use**  
- Print job status stuck on “Printing” or “Error”  
- Printer is online with no hardware faults  
- No paper jams or ink/toner issues

**Procedure**  
1. Press `Win + R`, type `services.msc`, and press Enter.  
2. Locate the **Print Spooler** service.  
3. Right-click the service and select **Restart**.  
4. While the service is stopped, navigate to:  
   `C:\Windows\System32\spool\PRINTERS`  
5. Delete all files inside the folder.  
6. Go to **Control Panel > Devices and Printers**.  
7. Right-click the affected printer and select **See what’s printing**.  
8. Ask the user to resend the print job.

**Post-Action – Verify Success**  
- Print job is removed from the queue  
- Printer begins printing  
- User confirms issue is resolved

**Escalation Criteria**  
- Spooler fails to restart  
- Printer unreachable via network  
- Error: "Driver unavailable" or similar driver issue

---

## SOP 2: Fixing Outlook Inbox Not Syncing (Clear OST Cache)

**Purpose**  
To resolve issues where the Outlook desktop app is connected but not receiving new emails.

**Tools & Access Required**  
- Access to the user’s PC or remote session  
- Admin rights to access and delete user data  
- Access to Outlook Web App (OWA) for comparison

**When to Use**  
- Outlook shows “Connected” but no new emails appear  
- OWA displays new emails  
- Issue is limited to one device

**Procedure**  
1. Verify Outlook is showing “Connected”.  
2. Ask user to log in to OWA (e.g., `https://outlook.office365.com`).  
3. If new emails appear in OWA, proceed.  
4. Close Outlook completely.  
5. Navigate to:  
   `C:\Users\[username]\AppData\Local\Microsoft\Outlook`  
6. Delete the `.ost` file (do not delete `.pst`).  
7. Reopen Outlook and allow mailbox to resync.

**Post-Action – Verify Success**  
- Inbox syncs and new emails appear  
- Test email is received successfully  
- No sync-related errors appear

**Escalation Criteria**  
- OWA also not receiving emails  
- Outlook fails to recreate the OST file  
- Error: “Data file cannot be accessed”

---

## SOP 3: Resetting a Locked or Expired User Account (Active Directory)

**Purpose**  
To restore access for users locked out of their account due to multiple failed login attempts or password expiry.

**Tools & Access Required**  
- Access to Active Directory Users and Computers (ADUC)  
- Helpdesk or Domain Admin rights  
- User’s full name or username

**When to Use**  
- Login error: “Account locked” or “Password expired”  
- User cannot log in despite correct credentials  
- Account exists in Active Directory

**Procedure**  
1. Open **Active Directory Users and Computers (ADUC)**.  
2. Use the search bar to find the user’s account.  
3. Right-click the account and select **Properties**.  
4. Under the **Account** tab:  
   - Uncheck **Account is locked out** (if checked)  
   - Click **Reset Password**  
   - Enter a secure temporary password  
   - Check **User must change password at next logon**  
5. Inform the user of the temporary password using a secure method.

**Post-Action – Verify Success**  
- User logs in with temporary password  
- Prompt appears to change password  
- User confirms successful login

**Escalation Criteria**  
- Account is disabled  
- Password reset fails  
- Account tied to system/service credentials  
- User unable to change password due to policy restrictions

---

