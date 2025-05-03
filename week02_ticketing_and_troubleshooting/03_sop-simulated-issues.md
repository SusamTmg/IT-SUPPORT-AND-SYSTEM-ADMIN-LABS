# 03 – SOPs for Simulated IT Issues

This document contains three Standard Operating Procedures (SOPs) created during Week 2 of my IT Support Lab Portfolio. Each SOP outlines a clear, structured method for resolving common IT issues based on simulated tickets in Jira Service Management.

These reflect the Tier 1 support tasks I practiced and demonstrate how I would approach these issues in a professional IT environment.

---

##  SOP 1: Clearing Stuck Print Jobs in Windows

** Purpose**  
Resolve issues where print jobs are stuck in the queue due to a frozen or corrupted print spooler service.

** Tools & Access Required**  
- Local or remote access to user’s device  
- Administrator rights  
- Familiarity with Windows Services and File Explorer

** When to Use**  
- Print job stuck on “Printing” or “Error”  
- Printer is online, with no hardware faults  
- No paper jams or ink/toner issues  

** Procedure**  
1. Press `Win + R`, type `services.msc`, and press Enter  
2. Locate the **Print Spooler** service  
3. Right-click → Restart  
4. While the service is stopped, go to:  
   `C:\Windows\System32\spool\PRINTERS`  
5. Delete all files in that folder  
6. Reopen print queue:  
   Control Panel → Devices and Printers → Right-click printer → “See what’s printing”  
7. Ask user to resend the print job

** Post-Action – Verify Success**  
- Print job leaves the queue  
- Printer starts printing  
- User confirms success

** Escalation Criteria**  
- Spooler fails to restart  
- Printer unreachable (network issue)  
- Driver errors (e.g., “Driver unavailable”)

---

##  SOP 2: Fixing Outlook Sync Issues (Clear OST Cache)

** Purpose**  
Resolve Outlook sync issues where the desktop app is connected but not receiving new emails.

** Tools & Access Required**  
- Access to the user’s PC or remote session  
- Admin rights (to delete local files)  
- Access to OWA for comparison

** When to Use**  
- Outlook shows “Connected” but inbox not updating  
- OWA shows new emails  
- Restarting Outlook didn’t help  

** Procedure**  
1. Confirm Outlook status shows **Connected**  
2. Ask user to log into [OWA](https://outlook.office365.com)  
3. If OWA shows latest emails:  
   - Close Outlook  
   - Navigate to:  
     `C:\Users\[username]\AppData\Local\Microsoft\Outlook`  
   - Delete the `.ost` file (do not touch `.pst`)  
   - Reopen Outlook  
4. Allow Outlook to resync with server

** Post-Action – Verify Success**  
- New emails appear in inbox  
- Send test email and verify delivery  
- No sync error messages

** Escalation Criteria**  
- OWA also fails to update  
- OST file won’t delete  
- Outlook fails to recreate OST  

---

##  SOP 3: Resetting Locked or Expired User Account (Windows/AD)

** Purpose**  
Restore access for users locked out due to incorrect password attempts or expired credentials.

** Tools & Access Required**  
- Active Directory Users and Computers (ADUC)  
- Helpdesk or Domain Admin rights  
- User’s full name or username

** When to Use**  
- Login error: “Account locked” or “Password expired”  
- Account exists in AD  
- User failed multiple login attempts  

** Procedure**  
1. Open ADUC  
2. Search for the user account  
3. Right-click → **Properties**  
4. Under **Account** tab:  
   - Uncheck **“Account is locked out”**  
   - Click **Reset Password**  
   - Set temporary secure password  
   - Check **“User must change password at next logon”**  
5. Notify user securely (not in plaintext email)

** Post-Action – Verify Success**  
- User logs in successfully  
- Prompted to change password  
- No further login issues  

** Escalation Criteria**  
- Account is disabled/corrupted  
- Reset fails (group policy block)  
- Account tied to system/service account  

---

