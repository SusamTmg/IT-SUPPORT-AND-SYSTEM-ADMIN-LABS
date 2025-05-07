# Ticketing System Visual Log

This document provides visual evidence of simulated IT support tickets managed in Jira Service Management as part of the IT Support Lab Portfolio. Each screenshot captures a specific stage of the support process, from ticket creation to resolution. The goal is to demonstrate a hands-on understanding of ticket handling, proper documentation, and professional communication within a typical helpdesk workflow.

Scroll down to view all screenshots with brief explanations of each step.


### **Ticket 1 – User Account Locked**
This screenshot captures a simulated Jira ticket where a user is unable to log in due to multiple failed login attempts. The issue was classified under the **Active Directory** component with **Medium** priority. A professional public reply was added to inform the user about the resolution process, while an internal note documents the investigation steps taken by the IT support technician.
![Image](https://github.com/user-attachments/assets/fdcdc9d3-249c-4792-815a-b89ebe36daa7)

---

### **Ticket 2 – VPN Not Connecting: Authentication Failed**

This set of screenshots captures a simulated ticket where the user was unable to connect to the company VPN due to authentication failure. The error message indicated incorrect credentials. The issue was resolved by checking VPN logs, resetting the user’s credentials in Active Directory, and confirming connectivity during follow-up.

A new service request is created in Jira for the VPN authentication issue, with a clear summary and detailed problem description provided by the user.

![Image](https://github.com/user-attachments/assets/609093a7-0b76-4146-a4cb-72dede3bd468) 
---

Internal note confirms credentials appear incorrect based on VPN logs. Status is set to "In Progress," and investigation begins.

![Image](https://github.com/user-attachments/assets/284802a5-8584-44c5-8000-cba26b4a37da) 
---

Technician documents steps taken: resetting VPN credentials, sending secure login details, and confirming successful reconnection from the user.

![Image](https://github.com/user-attachments/assets/a897e37c-b838-44b7-aab4-0f7adafb3535) 
---

The issue is marked as resolved. A clear and polite customer-facing reply informs the user that the VPN login has been restored and thanks them for their patience.

![Image](https://github.com/user-attachments/assets/276af275-6ab2-4232-9c1d-608ba3f8d80d)

---

### **Ticket 3 – VPN Connected, But Internal Apps Not Working**

This ticket demonstrates a situation where the user was able to establish a VPN connection using Cisco AnyConnect, but internal services such as Outlook and SharePoint were not accessible. The issue was diagnosed as a DNS or routing configuration problem. After verifying connectivity and eliminating local firewall issues, the ticket was escalated to the Networking team for further investigation.


Technician confirms the VPN tunnel is active but internal name resolution is failing. Suspects DNS or split tunneling and escalates the issue.

![image](https://github.com/user-attachments/assets/09c31742-4569-470d-b5bb-a2a6fea7953b)
---

This screenshot shows both the internal note and public response. The technician confirms that DNS resolution is failing after VPN connection is established and documents the decision to escalate the issue to the Networking team. A clear and polite message is sent to the user, explaining the issue and assuring timely updates from IT Support.

![Image](https://github.com/user-attachments/assets/37119909-767d-4552-a20f-535ca599a706)

---

### **Ticket 4 – Outlook Inbox Not Syncing: User Not Receiving Emails**

This ticket simulates an issue where Outlook Desktop is connected, but new emails are not appearing in the user's inbox. The user confirms that emails show up correctly in Outlook Webmail (OWA), suggesting a sync issue with the local Outlook app. The technician identifies a possible OST cache corruption, instructs the user to clear the cache, and confirms resolution after mailbox sync is restored.

The issue is created with a clear description and assigned a **High** priority. Internal notes show that OWA is working but Outlook isn’t syncing — pointing to a local cache issue. The technician initiates troubleshooting and monitors for results.

![Image](https://github.com/user-attachments/assets/0132036b-f761-4cad-b673-853bf1f8364e)
---

The user is asked to check Outlook Webmail and follow manual instructions to delete the OST file from the local system. This supports Outlook in rebuilding its local cache and resolving the sync error.
![Image](https://github.com/user-attachments/assets/1325a283-c1d0-4cd2-9190-66929a363614)
---

Once the issue is resolved and emails appear correctly in both Webmail and Outlook, the technician sends a polite closing message and marks the ticket as **Done**.
![Image](https://github.com/user-attachments/assets/8be80352-5966-4ed5-9a8f-62bad85061d3)

---

### **Ticket 5 – Print Job Not Printing: Shared Office Printer Issue**

This ticket simulates a common office issue where a print job is sent, but nothing is printed. The printer appears online with no error displayed, but the job remains in the print queue as “Printing” and never completes. The technician investigates the issue, confirms network connectivity, restarts the Print Spooler service, and successfully prints from an admin account.

The user reports a printing issue involving the HP LaserJet 402dne. The job is stuck in the queue without producing output. The ticket is assigned a **Medium** priority and placed in the queue for IT support.
![image](https://github.com/user-attachments/assets/98bdcece-4561-461a-b702-014bb272f293)
---

Internal notes show that the technician confirmed printer connectivity via IP, cleared the print queue, and restarted the Print Spooler service. A successful test print was performed.
![image](https://github.com/user-attachments/assets/85d51c60-7c0b-41b3-bbd5-ec92162a913b)
---

A professional user-facing comment is added explaining the resolution. The ticket is marked as **Done**, with continued monitoring if issues return.
![image](https://github.com/user-attachments/assets/d04e9d2e-8ec2-40dc-a6a8-68caf07e9007)

---

