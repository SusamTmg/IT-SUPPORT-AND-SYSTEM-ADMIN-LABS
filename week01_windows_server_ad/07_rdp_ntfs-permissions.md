# Lab 07 – Remote Desktop & NTFS Permissions

## RDP-Troubleshooting
**Objective:** Enable and troubleshoot Remote Desktop.

**Steps:**
- Enabled Remote Desktop on Client VM
- Verified Firewall settings for RDP
- Edited GPO to allow RDP (Remote Desktop Services > Connections)
- Added `john.smith` to Remote Desktop Users
- Verified in Group Policy: User Rights Assignment > Allow log on via RDP
- Tested RDP from Server to Client using mstsc

**Outcome:** Successfully logged in as `TECHSOLUTIONS\john.smith`


## File-Sharing
**Objective:** Create shared folder with NTFS permissions.

**Steps:**
- Created `C:\Shared_Folder` on Server
- Shared with `john.smith`, granted Full Control
- Set NTFS Permissions (Modify)
- Accessed from Client: `\\192.168.192.129\Shared_Folder`
- Created and edited files from both machines

**Learnings:** NTFS permissions provide fine control over file access.

