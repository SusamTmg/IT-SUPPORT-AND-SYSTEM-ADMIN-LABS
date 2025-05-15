# Lab Summary – Multi-DC Active Directory Infrastructure (IFM + RODC + Login Test)
This lab simulates a complete enterprise-level Active Directory (AD) setup. It includes promoting additional Domain Controllers using Install From Media (IFM), deploying a Read-Only Domain Controller (RODC), configuring password replication policies, creating and managing AD groups (such as VPN Users), and performing a login test from a Windows 10 client machine. These skills directly map to system administration and IT support tasks in distributed environments.

---
### **Fig 1.0: Domain Controller Info – IP Configuration**
The ipconfig command is run on PLABDC01 to display its static IP configuration. This verifies that the server is properly networked and ready to act as the primary Domain Controller.
Confirming the IP address, gateway, and DNS is critical before adding any new DCs or clients to the domain.

![image](https://github.com/user-attachments/assets/d66e2e94-a311-4a34-abd1-e45a1080dc02)

---
### **Fig 1.1: IFM Media Creation with ntdsutil**
A command is executed in the Command Prompt on PLABDC01 using ntdsutil to create Install From Media (IFM). This generates a copy of Active Directory data that will later be used to promote another server (PLABDM01) without requiring full replication.
IFM is used in real enterprises to save bandwidth and time when promoting DCs in remote or isolated networks.

![image](https://github.com/user-attachments/assets/221ac8f2-503f-42cf-a4cf-e89df14ce187)

---
### **Figure 1.2: Successful IFM Media Output**
This screenshot shows the ongoing IFM media creation process in Command Prompt on PLABDC01. It confirms the tool is successfully exporting the Active Directory database and SYSVOL folder into the specified path.

![image](https://github.com/user-attachments/assets/04349aed-7169-4c34-95c0-ace9141a5339)

---
### **Figure 1.3: Mapping Network Drive from PLABDM01**
On PLABDM01, the Map Network Drive window is open to connect to a shared folder containing the IFM media from PLABDC01.
This step allows PLABDM01 to access the required IFM files across the network, needed for its domain promotion.

![image](https://github.com/user-attachments/assets/b244ebed-d304-451f-893f-5fd5a90f9eae)

---
### **Figure 1.4: Verifying ADDS Role on PLABDM01**
PowerShell confirms that the Active Directory Domain Services role has been successfully installed on PLABDM01. This prepares it for promotion to a full Domain Controller using the IFM data.

![image](https://github.com/user-attachments/assets/c856b62d-6815-4570-af06-a8d515cdfde1)

---
### **Figure 1.5: PLABDM01 DC Promotion – Domain Controller Options**
The Domain Services Configuration Wizard is used on PLABDM01 to begin the promotion. The options page prompts for the DSRM password and role settings.
The Directory Services Restore Mode (DSRM) password is critical for system recovery operations.

![image](https://github.com/user-attachments/assets/b366574f-28e0-40f4-94d4-b11edd5eed9b)

---
### **Figure 1.6: Prerequisite Check Before DC Promotion**
The AD DS Configuration Wizard ran prerequisite checks before promoting PLABDM01 to DC. No critical errors are found, allowing promotion to continue.

![image](https://github.com/user-attachments/assets/433b74e6-23c5-4df6-8a49-c1914c611159)

---
### **Figure 1.7: ADUC View on PLABDM01**
The Active Directory Users and Computers (ADUC) console is open on PLABDM01, confirming that it has successfully been promoted to a Domain Controller and is now managing domain objects.
This confirms replication from PLABDC01 is working and PLABDM01 is fully integrated.

![image](https://github.com/user-attachments/assets/c79525ee-fa36-4fcd-aba9-719491716add)

---
### **Figure 1.8: Verifying AD Services via PowerShell**
PowerShell is used on PLABSA01 to confirm that Active Directory Domain Services were successfully installed. This prepares PLABSA01 for Read-Only Domain Controller (RODC) promotion.

![image](https://github.com/user-attachments/assets/f6942cb8-362a-447e-8c97-a1de992e1fc9)

---
### **Figure 1.9: Credential Prompt During RODC Setup**
While promoting the RODC, a credential dialog box appears in PowerShell, requiring administrative credentials from the domain (practicelabs\administrator).

![image](https://github.com/user-attachments/assets/ecba7b2a-c32a-4797-bba9-3bfffb5de944)

---
### **Figure 1.10: PowerShell Prompt Before RODC Promotion**
PLABSA01 is now running a PowerShell command to promote itself as an RODC. The prompt is asking to confirm whether to proceed with the installation.
RODCs are often used in branch offices to improve login speed while limiting security risks.

![image](https://github.com/user-attachments/assets/6760667a-e760-47aa-8ab9-50b40fe0b241)

---
### **Figure 1.11: ADUC View on PLABSA01**
The ADUC console now displays PLABSA01 within the domain’s Computers container, confirming the successful Read-Only Domain Controller promotion.

![image](https://github.com/user-attachments/assets/f85cb539-b695-4a6e-b223-98c529c52c69)

---
### **Figure 1.12: IP Config Rechecked on RODC**
A second ipconfig command run on PLABSA01 confirms its network configuration and ensures that it's reachable within the domain for replication and login services.

![image](https://github.com/user-attachments/assets/4be47ff8-fc01-4736-ac2a-e906fca79a0c)

---
### **Figure 1.13: RODC Password Replication Group Properties**
I opened group properties to manage which users can have passwords cached on RODC, controls who can log in through the RODC when it is offline or disconnected.

![image](https://github.com/user-attachments/assets/eba0f9f0-45c8-4438-806a-72f9ed7cafff)

---
### **Figure 1.14: Creating a New Security Group**
A new group named VPN Users is being created in ADUC. This group will later be used to define specific access permissions and password replication rights.

![image](https://github.com/user-attachments/assets/b4abc360-8acb-43a1-a98f-731a2e7a13aa)

---
### **Figure 1.15: VPN Users Group Properties**
The VPN Users security group properties show that specific domain users have been added as members — likely those who need cached credentials at remote sites.

![image](https://github.com/user-attachments/assets/ff834b63-c486-4863-9efc-cf0842ab28f2)

---
### **Figure 1.16: Allow Passwords to Be Cached on RODC**
The Add Groups, Users and Computers dialog is used to include the VPN Users group in the RODC’s password replication scope.
This ensures the RODC can locally cache the credentials of users in this group — important for offline logins.

![image](https://github.com/user-attachments/assets/5780c7e4-a4fe-4809-aeaf-f0c3152a247d)

---
### **Figure 1.17: PLABSA01 Properties – Cached Credentials**
The Properties dialog for PLABSA01 is open, showing which users/groups are allowed to have their passwords cached by the RODC.

![image](https://github.com/user-attachments/assets/0a48ce19-4a1f-448a-a506-c93d5e63cdc8)

---
### **Figure 1.18:Advanced Password Replication Policy on RODC**
The Advanced Password Replication Policy window shows current entries for which user credentials are allowed or denied on the RODC.

![image](https://github.com/user-attachments/assets/ebbe4b1d-a75f-49f4-8876-8db7e565f75e)

---
### **Figure 1.19: Advanced PRP Audit – RODC Credential Caching**
This screenshot shows the VPN Users group confirmed in the Allowed list, which ensures that users can log in even if the connection to the main DC is unavailable.

![image](https://github.com/user-attachments/assets/10504209-1c65-4155-b27d-4bcd6dd195cd)

---
### **Figure 1.20: Final View of PRP Configuration**
The policy dialog confirms successful configuration of the Allowed and Denied lists for password caching on PLABSA01.

![image](https://github.com/user-attachments/assets/25d61092-2ee9-4331-9c6c-c5625bb9eff4)

---
### **Figure 1.21: Login Test on PLABWIN10**
A Windows 10 client machine (PLABWIN10) attempts login using susam.tamang, a domain user. The fact that the RODC handles this login proves that PRP and replication are functioning correctly.
This final step simulates a real-world remote login scenario where cached credentials allow successful authentication without needing to contact the main DC.

![image](https://github.com/user-attachments/assets/21a7a30b-dcd4-4e02-8e22-9b6285c92912)


