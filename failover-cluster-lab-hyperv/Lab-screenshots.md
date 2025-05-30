# High Availability Infrastructure Lab with Hyper-V, Failover Clustering, and iSCSI

This lab project demonstrates the setup of a fully functional enterprise-grade high availability (HA) infrastructure using Windows Server, Hyper-V, Failover Clustering, and iSCSI-based shared storage. 

The simulation was performed in a nested virtualization environment with four virtual machines:  
- `TamangDC` (Domain Controller),  
- `TamangStorage` (iSCSI Target Server),  
- `TamangVH1` and `TamangVH2` (Hyper-V nodes and cluster members).

Key configurations include:
- Enabling nested virtualization
- Installing and configuring Hyper-V on all nodes
- Setting up Active Directory and DNS
- Creating and mapping shared storage with iSCSI
- Building a failover cluster with live migration support
- Testing high availability of virtual machines across nodes

Each section below includes step-by-step PowerShell commands, explanations, and screenshots verifying successful implementation. This project was built to simulate real-world enterprise infrastructure and demonstrate core system administration skills relevant to IT Support, SysAdmin, and Infrastructure roles.

---


## Creating the Public Virtual Switch

![Image](https://github.com/user-attachments/assets/c4c97cd9-54f2-4daa-a1c0-96f055cc8342)

This screenshot shows the creation of the public virtual switch `TamangSwitch` using PowerShell. It is used for general communication between all four VMs: TamangDC, TamangStorage, TamangVH1, and TamangVH2.

**Key actions:**
- Created an internal switch for VM communication
- Named the switch `TamangSwitch`
- Used PowerShell command:  
  `New-VMSwitch -SwitchName "TamangSwitch" -SwitchType Internal`

---

## Creating 4 VMs via PowerShell Automation

![image](https://github.com/user-attachments/assets/d2b030cd-4962-4d8a-b051-c144d8acbeef)

This script provisions four VMs (TamangDC, TamangStorage, TamangVH1, TamangVH2) with specific CPU, RAM, and disk sizes. It uses loops and arrays to automate creation and startup, simulating real-world infrastructure automation.

**Key actions:**
- Assigned ISO for Windows Server installation
- Defined hardware specs per VM
- Automatically started all VMs with consistent config

---

## Configuring Boot Order for ISO Installation

![image](https://github.com/user-attachments/assets/b203b46a-4ba1-4297-885c-478704902863)


![image](https://github.com/user-attachments/assets/1469e157-b59b-4ea8-b1da-139a5dc46a49)


Each VM was configured in Hyper-V Manager to boot from the attached ISO by moving the DVD drive to the top of the boot order.

**Key actions:**
- Accessed firmware settings of each VM
- Set DVD Drive (ISO) as the primary boot option
- Ensured proper OS installation from ISO

---

## Creating Storage and Heartbeat Virtual Switches

![image](https://github.com/user-attachments/assets/a2b9745e-77d8-4b11-bb11-391ffba8a241)


This screenshot shows the creation of two new virtual switches using PowerShell:
- `TamangStorage` for iSCSI communication
- `TamangHeartbeat` for cluster heartbeat monitoring

These internal switches are essential for ensuring dedicated traffic channels for storage access and failover detection.

---

## Attaching NICs to VMs for Storage and Heartbeat

![image](https://github.com/user-attachments/assets/b49c97df-a413-4f1c-9bf1-97b6d2ddbefb)


PowerShell commands were used to attach new NICs to each VM and bind them to the `TamangStorage` and `TamangHeartbeat` switches. This allows each VM to access shared storage and participate in cluster health checks.

---

## Attaching Heartbeat NICs to VMs

![image](https://github.com/user-attachments/assets/766ca0ad-c71f-4990-ba0f-4d85d619b5b5)


This step adds the heartbeat NICs to each VM for private communication between the nodes (VH1 and VH2) to detect failure and maintain cluster stability.

---

## Verifying NIC Configuration on All VMs

![image](https://github.com/user-attachments/assets/a501d3b9-8ea1-4322-96fa-a71666d30578)


A PowerShell command was used to verify that each VM has all three NICs:
- `TamangSwitch` (Public network)
- `TamangStorage` (Storage access)
- `TamangHeartbeat` (Cluster heartbeat)

This ensures proper network segmentation and confirms NIC setup before cluster configuration.

---

## Assign Static IP to TamangStorage VM

![image](https://github.com/user-attachments/assets/3f3f9426-aca8-4c74-aaf8-64fd260f077d)

This screenshot shows the assignment of a static storage IP `192.168.111.101` to the `Ethernet 2` adapter inside the TamangStorage VM using PowerShell. This allows the VM to communicate over the storage network with other nodes in the cluster.

**Key actions:**  
- Interface alias: `Ethernet 2`  
- Assigned IP: `192.168.111.101`  
- Subnet prefix length: `24`  
- Used PowerShell command:  
  `New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 192.168.111.101 -PrefixLength 24`

---

## Assign Static IP to TamangVH1 (Storage)

![image](https://github.com/user-attachments/assets/e8a877e4-aaf9-42a9-8a37-5dcfe16abb4d)

This screenshot shows the assignment of a static IP `192.168.111.101` to the `Ethernet 2` adapter inside the TamangVH1 VM. This step ensures VH1 can connect to the same storage network for shared access.

**Key actions:**  
- Interface alias: `Ethernet 2`  
- Assigned IP: `192.168.111.101`  
- Subnet prefix length: `24`  
- Used PowerShell command:  
  `New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 192.168.111.101 -PrefixLength 24`

---

## Assign Heartbeat IP to TamangVH1

![image](https://github.com/user-attachments/assets/30b9a5bc-bdd2-4203-a139-4780505ac910)

This screenshot shows the assignment of a heartbeat IP `192.168.222.101` to `Ethernet 3` in TamangVH1. The heartbeat network is used for cluster health checks between nodes.

**Key actions:**  
- Interface alias: `Ethernet 3`  
- Assigned IP: `192.168.222.101`  
- Subnet prefix length: `24`  
- Used PowerShell command:  
  `New-NetIPAddress -InterfaceAlias "Ethernet 3" -IPAddress 192.168.222.101 -PrefixLength 24`

---

## Assign Static IP to TamangVH2 (Storage)

![image](https://github.com/user-attachments/assets/fb0fa86c-66fd-48c3-b675-fbcd9ccc9c6d)

This screenshot shows the assignment of static IP `192.168.111.102` to `Ethernet 2` inside TamangVH2. This connects it to the shared storage network for clustering.

**Key actions:**  
- Interface alias: `Ethernet 2`  
- Assigned IP: `192.168.111.102`  
- Subnet prefix length: `24`  
- Used PowerShell command:  
  `New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 192.168.111.102 -PrefixLength 24`

---

## Assign Heartbeat IP to TamangVH2

![image](https://github.com/user-attachments/assets/a515ead8-2155-4a26-b379-39cc16c9f04f)

This screenshot shows the assignment of a heartbeat IP `192.168.222.102` to `Ethernet 3` in TamangVH2 for cluster monitoring and node communication.

**Key actions:**  
- Interface alias: `Ethernet 3`  
- Assigned IP: `192.168.222.102`  
- Subnet prefix length: `24`  
- Used PowerShell command:  
  `New-NetIPAddress -InterfaceAlias "Ethernet 3" -IPAddress 192.168.222.102 -PrefixLength 24`

---

## Assign Host IP for Internal Communication

![image](https://github.com/user-attachments/assets/b5a9d736-2017-411f-8516-ba526cdeafd4)

This screenshot shows the host machine being configured with IP `172.50.39.1` for the internal switch `TamangSwitch`, which allows communication between the host and VMs over an internal network.

**Key actions:**  
- Interface alias: `Ethernet (TamangSwitch)`  
- Assigned IP: `172.50.39.1`  
- Subnet prefix length: `24`  
- Used PowerShell command:  
  `New-NetIPAddress -InterfaceAlias "Ethernet (TamangSwitch)" -IPAddress 172.50.39.1 -PrefixLength 24`

---

## Testing IP Connectivity Between All Nodes

![image](https://github.com/user-attachments/assets/34b81a96-2bb7-42eb-9dd5-8b862b2b0f06)
![image](https://github.com/user-attachments/assets/0c6dd9bd-a3ee-4f88-9cde-c1f246438e0d)

The screenshot shows ping test results between all VMs and the host to confirm successful static IP configuration and communication across storage and heartbeat networks.

**Key actions:**  
- Pinged storage and heartbeat IPs of each VM  
- Verified bidirectional communication  
- Confirmed zero packet loss in all ping responses

  ---

## Enable Nested Virtualization on TamangVH1, TamangVH2, and TamangStorage

![image](https://github.com/user-attachments/assets/c46ae2e2-4f3e-4c4d-8420-b6b7f5d23828)
![image](https://github.com/user-attachments/assets/e20f6c81-2d7c-48d9-9ddf-7df424efacbe)

Before installing Hyper-V on the virtual machines, nested virtualization must be enabled to allow VMs to run additional VMs inside them. This simulates enterprise-level environments and is essential for running lab scenarios involving clustering, replication, and high availability.

**Why it matters:**  
Nested virtualization is commonly used in modern enterprise test environments. It allows IT professionals to simulate full-stack infrastructure (e.g., host-hypervisor-guest) on a single physical machine for development, support training, and disaster recovery testing.

**Key actions performed:**  
- Enabled virtualization extensions on:
  - `TamangVH1`
  - `TamangVH2`
  - `TamangStorage`
- Used PowerShell commands on the host:
  ```
  Set-VMProcessor -VMName "TamangVH1" -ExposeVirtualizationExtensions $true
  Set-VMProcessor -VMName "TamangVH2" -ExposeVirtualizationExtensions $true
  Set-VMProcessor -VMName "TamangStorage" -ExposeVirtualizationExtensions $true
  ```

---

## Install Hyper-V on TamangVH1

![image](https://github.com/user-attachments/assets/6f277d42-bb68-4946-9f5e-0c7aa9c375ee)

TamangVH1 was configured as a Hyper-V host by installing the Hyper-V role and management tools. This enables the VM to host and manage nested virtual machines.

**Why it matters:**  
Installing Hyper-V on a virtualized VM is a key skill for simulating host-level infrastructure, performing guest VM testing, and practicing clustering or replication in a fully isolated environment.

**Key actions performed:**  
- Installed Hyper-V role using PowerShell:
  ```
  Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
  ```
- Restarted the system to apply changes

---

## Install Hyper-V on TamangVH2

![image](https://github.com/user-attachments/assets/2dfc02a6-a8f5-410c-9eb0-22a0dd546d25)

TamangVH2 was also set up as a Hyper-V host to support multi-host configurations, such as clustering or failover testing in lab environments.

**Why it matters:**  
Enabling multiple Hyper-V nodes prepares the environment for advanced scenarios like high availability, live migration, and Hyper-V Replica — all important concepts in system administration.

**Key actions performed:**  
- Ran installation via PowerShell:
  ```
  Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
  ```
- Allowed the VM to reboot automatically after setup

---

## Install Hyper-V on TamangStorage

![image](https://github.com/user-attachments/assets/1095d1c9-e9cb-49ab-8be8-9f28ea333b3c)
![image](https://github.com/user-attachments/assets/d81f8532-605d-4791-8481-242aa1ed5205)

The Hyper-V role was installed on TamangStorage to allow the use of VM-based storage replication, backups, and shared virtual disks in cluster simulations.

**Why it matters:**  
Adding Hyper-V to the storage server opens the possibility of configuring file-based storage, VM migration targets, and even nested lab storage clusters, mirroring real enterprise designs.

**Key actions performed:**  
- Installed Hyper-V role via PowerShell:
  ```
  Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
  ```
- Verified installation through Server Manager dashboard

  ---

  ## Install Active Directory Domain Services (AD DS)

![image](https://github.com/user-attachments/assets/96f62f66-9583-4c04-a3d0-82ef2accd0e4)

The first step in creating a Domain Controller is to install the AD DS role. This was done using PowerShell to ensure consistency and repeatability across deployments.

**Why it matters:**  
Installing AD DS prepares the server for domain controller promotion, enabling centralized identity management and group policy enforcement — critical in any enterprise network.

**Key actions performed:**  
- Ran the following PowerShell command:  
  ```
  Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
  ```
- Verified successful installation of the role

---

## Promote Server to Domain Controller and Create Domain

![image](https://github.com/user-attachments/assets/f907fb78-f499-4f03-9dc6-2b620acd6a31)

The server was promoted to a Domain Controller and configured to create a new root domain: `tamang.local`. This was completed using PowerShell with the `Install-ADDSForest` cmdlet.

**Why it matters:**  
Promoting a server to a Domain Controller is foundational to building secure, scalable Windows networks. It provides the backbone for authentication, authorization, DNS, and directory-based configuration.

**Key actions performed:**  
- Created a new forest using:  
  ```
  Install-ADDSForest -DomainName "tamang.local"
  ```
- Triggered automatic reboot after promotion

---

## Verify Domain Controller Setup

![image](https://github.com/user-attachments/assets/8898306e-d859-462a-9325-14ac98110186)

After rebooting, verification was performed to ensure the domain controller was fully functional.

**Why it matters:**  
Verifying the Domain Controller ensures that the domain services are properly installed and configured, which is essential before joining other machines to the domain.

**Key actions performed:**  
- Ran the command:
  ```
  Get-ADDomain
  ```
- Confirmed domain name, NetBIOS name, forest, and replication configuration

---

## Verify DNS Server Functionality

![image](https://github.com/user-attachments/assets/5b93fbff-7bcd-4cea-9064-990b124b0b84)

A PowerShell query was used to inspect DNS records and validate that the Domain Controller is properly resolving hostnames.

**Why it matters:**  
AD-integrated DNS is essential for domain-joined systems to locate controllers, services, and replicate properly. Any DNS failure can disrupt login, policy, and trust.

**Key actions performed:**  
- Used command:
  ```
  Get-DnsServerResourceRecord
  ```
- Verified presence of A, NS, and SRV records for the `tamang.local` domain

---

## Join Other VMs to the Domain (TamangStorage, TamangVH1, TamangVH2)

![image](https://github.com/user-attachments/assets/59445c0b-9118-489e-9996-d6f4ffba5275)
![image](https://github.com/user-attachments/assets/98c3fb5f-e8e5-4ae0-a58d-63a01a7e4f42)

Each VM was joined to the newly created `tamang.local` domain using PowerShell and domain administrator credentials.

**Why it matters:**  
Joining systems to a central domain allows for unified login, GPO enforcement, and network-wide access control — all core responsibilities of a system administrator.

**Key actions performed:**  
- Ran this command on each VM:
  ```
  Add-Computer -DomainName "tamang.local"
  ```
- Authenticated using domain admin credentials  
- Restarted the systems to complete the domain join process

---

## Setup and Prepare Storage Server (TamangStorage)

![image](https://github.com/user-attachments/assets/699a8b87-7bca-415c-8554-f4d63f79f887)

To allow VH1 and VH2 to use shared storage for clustering and replication, TamangStorage was configured as an iSCSI Target Server using PowerShell.

**Why it matters:**  
Shared storage via iSCSI is essential in enterprise environments for high availability and live migration. Configuring an iSCSI target server simulates SAN environments used in datacenters.

**Key actions performed:**  
- Installed iSCSI Target Server role:
  ```
  Install-WindowsFeature FS-iSCSITarget-Server
  ```
- Confirmed installation was successful in PowerShell

---

## Create Virtual Disk for iSCSI Storage

![image](https://github.com/user-attachments/assets/04d3a07e-2b49-4bd1-bf82-46938c46a13f)

A virtual hard disk (VHDX) was created on TamangStorage to be shared between VH1 and VH2 using the iSCSI protocol.

**Why it matters:**  
Creating a virtual disk simulates a shared LUN. This step is critical for failover clustering or building shared storage systems.

**Key actions performed:**  
- Created a VHDX file using PowerShell:
  ```
  New-IscsiVirtualDisk -Path "C:\ClusterStorage.vhdx" -Size 50GB
  ```

---

## Configure iSCSI Initiator on VH1 and VH2

![image](https://github.com/user-attachments/assets/6344c86c-1824-4f40-a33b-d89940c768eb)
![image](https://github.com/user-attachments/assets/7b3d0e7b-f378-43b8-866c-00b3dc18f1ba)

Before connecting to shared storage, VH1 and VH2 were configured as iSCSI initiators. Services were started, and IQNs were retrieved.

**Why it matters:**  
This step identifies the unique iSCSI names of VH1 and VH2, which are needed to securely map virtual disks to only those systems.

**Key actions performed:**  
- Enabled and started the iSCSI service:
  ```
  Set-Service -Name MSiSCSI -StartupType Automatic
  Start-Service -Name MSiSCSI
  ```
- Retrieved IQN using:
  ```
  Get-InitiatorPort
  ```

---

## Create iSCSI Target for VH1 and VH2

![image](https://github.com/user-attachments/assets/951cadcb-574c-4486-85d1-ec2fa321d9ed)

A secure iSCSI target was created on TamangStorage, mapped only to VH1 and VH2 using their IQNs. This ensures only authorized systems can access the shared disk.

**Why it matters:**  
Mapping by IQN prevents unauthorized systems from accessing critical shared storage. This mimics real-world SAN security setups.

**Key actions performed:**  
- Created an iSCSI target:
  ```
  New-IscsiServerTarget -TargetName "TamangClusterTarget" -InitiatorIds "IQN:iqn.vh1", "IQN:iqn.vh2"
  ```
- Mapped the shared VHDX disk:
  ```
  Add-IscsiVirtualDiskTargetMapping -TargetName "TamangClusterTarget" -Path "C:\ClusterStorage.vhdx"
  ```

---

## Connect iSCSI Target from VH1 and VH2

VH1:
![image](https://github.com/user-attachments/assets/69f6e316-1f1d-4d06-b809-c32964dd24da)
![image](https://github.com/user-attachments/assets/964b0e96-b5f3-4b99-a099-0e8cdbd546b9)

VH2:
![image](https://github.com/user-attachments/assets/b92e316f-73e5-4994-a07a-44c7759580aa)

The iSCSI target was discovered and connected from VH1 and VH2 using PowerShell.

**Why it matters:**  
This step validates the iSCSI communication path. Without it, clustering or storage operations would fail due to missing shared volumes.

**Key actions performed:**  
- Discovered target portal:
  ```
  New-IscsiTargetPortal -TargetPortalAddress 192.168.111.3
  ```
- Viewed discovered targets:
  ```
  Get-IscsiTarget
  ```
- Connected to the iSCSI target:
  ```
  Connect-IscsiTarget -NodeAddress "iqn.vh1...tamang.local" -IsPersistent $true
  ```

---

## Verify iSCSI Connection on VH1 and VH2

![image](https://github.com/user-attachments/assets/feb06627-09bc-4fc8-890f-7da77f61f864)
![image](https://github.com/user-attachments/assets/cde5901d-9673-4496-8c6e-cd6799ce5f16)

Verification was done on both VH1 and VH2 to ensure they were connected to the shared iSCSI target with persistent sessions.

**Why it matters:**  
This ensures that both nodes have proper access to shared storage, which is critical before enabling clustering or live migration scenarios.

**Key actions performed:**  
- Ran:
  ```
  Get-IscsiSession
  ```
- Verified session state, authentication, and persistence

---

## Prepare Disk on VH1 (Format and Ready for Cluster Use)

![image](https://github.com/user-attachments/assets/14a8490d-ad1b-40fa-9476-c9a6a9efe74d)

After connecting to the iSCSI shared storage, the new disk appeared in VH1. The disk was checked, brought online, and initialized with the GPT partition style.

**Why it matters:**  
Disks must be online and initialized before they can be partitioned or formatted. GPT is used to support larger disks and modern partition layouts suitable for clustering.

**Key actions performed:**  
- Ran the following commands in PowerShell:
  ```
  Get-Disk
  Set-Disk -Number 1 -IsOffline $false
  Initialize-Disk -Number 1 -PartitionStyle GPT
  ```

---

## Create Partition and Format for Cluster Storage

![image](https://github.com/user-attachments/assets/766f27a6-c7e2-4ac5-9581-3c71cf8c52a5)

A new NTFS volume was created using the full size of the shared disk and labeled as `ClusterDisk`. This volume will later be used for Failover Cluster shared storage.

**Why it matters:**  
Clustering requires the shared disk to be formatted and accessible with a label. NTFS is the required file system for most Windows-based clustering scenarios.

**Key actions performed:**  
- Created a new partition:
  ```
  New-Partition -DiskNumber 1 -UseMaximumSize -AssignDriveLetter
  ```
- Formatted the volume with NTFS:
  ```
  Get-Volume -DriveLetter E | Format-Volume -FileSystem NTFS -NewFileSystemLabel "ClusterDisk" -Confirm:$false
  ```

---

## Verify Disk Health and Volume Status

![image](https://github.com/user-attachments/assets/a589f623-9d19-4546-81de-7b69dc338289)

The volume status was checked to ensure the disk was healthy and ready for use in Failover Cluster configuration.

**Why it matters:**  
Before adding shared disks to a cluster, the disk must be properly formatted and show as “Healthy”. Any issues here would prevent clustering or shared access.

**Key actions performed:**  
- Verified volume using:
  ```
  Get-Volume
  ```

---

## Create VHDX via Hyper-V Wizard (Alternative Method)

![image](https://github.com/user-attachments/assets/7f51004e-b09e-489b-9033-bb1e4805ce7c)
![image](https://github.com/user-attachments/assets/0dcd768c-9cb3-4750-93dd-ceb94da59246)
![image](https://github.com/user-attachments/assets/7721be87-ba45-4835-a430-b8be831b99f7)

An alternative method was used to create VHDX storage using the Hyper-V Manager GUI. This approach is commonly used by admins preferring visual setup over CLI scripting.

**Why it matters:**  
Hyper-V Manager provides a user-friendly way to configure shared VHDX storage when working in lab or mixed environments. This flexibility is useful for junior admins or training scenarios.

**Note:**  
> *The path to the virtual disk was changed to `C:\iSCSIVirtualDisks\` after the screenshot.*

---

## Reinstall iSCSI Role with All Management Tools (Optional Step)

![image](https://github.com/user-attachments/assets/af2bda7a-3062-4060-adc1-9a8df5947cd4)

To ensure all necessary subfeatures and GUI tools are included, the iSCSI Target role was optionally reinstalled with full management features.

**Why it matters:**  
Installing the role with all subfeatures ensures access to PowerShell and GUI tools for managing iSCSI sessions, targets, and VHDX mappings.

**Key actions performed:**  
- Ran this command:
  ```
  Install-WindowsFeature -Name FS-iSCSITarget-Server -IncludeAllSubFeature -IncludeManagementTools
  ```
  
---

## Connect VH1 and VH2 to Shared iSCSI Storage via Initiator

![image](https://github.com/user-attachments/assets/c303b890-f8f8-4e7d-b328-843899973310)
![image](https://github.com/user-attachments/assets/ea120df9-08e4-49c3-ab69-0e3c03c29cb5)
![image](https://github.com/user-attachments/assets/b04b7e81-20fd-4036-871c-141596b37910)

iSCSI initiator was used inside VH1 and VH2 to connect to the storage disks provided by TamangStorage. The graphical interface was used to verify and configure target connections.

**Why it matters:**  
iSCSI enables shared storage in environments where physical SANs are unavailable. It's a key skill for system administrators working with virtual clusters or testing HA setups.

**Key actions performed:**  
- Launched iSCSI Initiator GUI  
- Discovered targets provided by `TamangStorage`  
- Connected and confirmed sessions

---

## Create Additional Storage Disks on Host and Attach to TamangStorage

![image](https://github.com/user-attachments/assets/b3450f7b-6356-4f7d-a559-40a8bb053e8c)
![image](https://github.com/user-attachments/assets/b199284b-c9dc-4c22-960e-d6a681cceecc)

Two 4GB virtual disks were created and attached to the `TamangStorage` VM. This was done from the Hyper-V host machine.

**Why it matters:**  
Multiple disks simulate real-world scenarios for failover clustering, including quorum disks and shared volumes for live migration.

**Key actions performed:**  
- Used Hyper-V Manager to:
  ```
  New-VHD -Path "C:\VHDs\StorageDisk1.vhdx" -SizeBytes 4GB -Dynamic
  New-VHD -Path "C:\VHDs\StorageDisk2.vhdx" -SizeBytes 4GB -Dynamic
  ```
- Attached both VHDs to the `TamangStorage` VM settings

---

## Initialize Disks and Create iSCSI Targets

![image](https://github.com/user-attachments/assets/f5b90630-082a-416b-86ee-4d99fd7c1e57)

The new VHDs were brought online and initialized, and two new iSCSI targets were created using PowerShell on `TamangStorage`.

**Why it matters:**  
This prepares each virtual disk to be individually mapped to specific target names (E and F), helping organize how clustering nodes connect to shared storage.

**Key actions performed:**  
- Reinstalled iSCSI Target Server role:
  ```
  Install-WindowsFeature -Name FS-iSCSITarget-Server -IncludeAllSubFeature -IncludeManagementTools
  ```

---

## Configure iSCSI Target for Disk E

![image](https://github.com/user-attachments/assets/28028389-fe5e-4483-a239-79359e8e3693)

iSCSI Target "ISCSI-E" was created for shared disk E, with initiator IPs of VH1 and VH2.

**Key actions performed:**  
```
New-IscsiServerTarget -TargetName "ISCSI-E" -InitiatorIds @("IPAddress:192.168.111.101","IPAddress:192.168.111.102")
New-IscsiVirtualDisk -Path "E:\ISCSI-E.vhdx" -Size 4GB
Add-IscsiVirtualDiskTargetMapping -TargetName "ISCSI-E" -Path "E:\ISCSI-E.vhdx"
```

---

## Configure iSCSI Target for Disk F

![image](https://github.com/user-attachments/assets/e847b765-9114-4010-8b2f-b8424a6bf643)

Another iSCSI Target "ISCSI-F" was configured for a second virtual disk.

**Key actions performed:**  
```
New-IscsiServerTarget -TargetName "ISCSI-F" -InitiatorIds @("IPAddress:192.168.111.101","IPAddress:192.168.111.102")
New-IscsiVirtualDisk -Path "F:\ISCSI-F.vhdx" -Size 4GB
Add-IscsiVirtualDiskTargetMapping -TargetName "ISCSI-F" -Path "F:\ISCSI-F.vhdx"
```

---

## Connect iSCSI Targets from VH1

![image](https://github.com/user-attachments/assets/7c4b1b8b-b0cd-402d-841f-a53cfb8ffe5c)
![image](https://github.com/user-attachments/assets/f2626a2c-9cac-48d7-b9ad-210a9d6f63d5)
![image](https://github.com/user-attachments/assets/e0ad1e00-8ae2-418b-8897-8b7c87f1c662)


From VH1, both "ISCSI-E" and "ISCSI-F" targets were discovered and connected using the iSCSI Initiator GUI.

**Key actions performed:**  
- Launched iSCSI Initiator  
- Performed Quick Connect and confirmed sessions  
- Opened Disk Management and brought disks online

---

## Verify iSCSI Disks on VH1

![image](https://github.com/user-attachments/assets/a8397d3a-8123-4423-9645-25eb87d4964c)
![image](https://github.com/user-attachments/assets/1722dbfb-c936-4217-b3a7-13f5d11f8d4c)
![image](https://github.com/user-attachments/assets/6c8e5a33-5fe1-4bc8-a740-e3a581b77fe2)



Disk Management showed both disks successfully connected and ready to be initialized and used.

**Key actions performed:**  
- Brought disks online  
- Checked in File Explorer that both drives are listed

---

## Repeat Process for VH2 and Verify

![image](https://github.com/user-attachments/assets/722870d0-572a-4fac-8ea5-229fd035eeb2)

VH2 repeated the same iSCSI discovery, connection, and disk mounting process. Both E and F drives appeared under Disk Management and File Explorer.

**Key actions performed:**  
- Verified both iSCSI targets connected  
- Confirmed disks are visible in Explorer and healthy

---

## Create Cluster Clustering Failover

![image](https://github.com/user-attachments/assets/70567bad-23c5-4c98-8f83-5482e1639202)

To prepare for cluster failover, the following roles were installed inside both `TamangVH1` and `TamangVH2`:
- iSCSI Target Server  
- Failover Clustering  
- Multipath-IO  

**Key actions:**
- Installed required features for high-availability setup using PowerShell:
  ```
  Install-WindowsFeature -Name FS-iSCSITarget-Server -IncludeAllSubFeature -IncludeManagementTools  
  Install-WindowsFeature -Name Failover-Clustering -IncludeManagementTools  
  Install-WindowsFeature -Name Multipath-IO  
  ```

---

## Create Failover Cluster in Failover Cluster Manager

![image](https://github.com/user-attachments/assets/afa5958f-0703-4c95-acc0-8ca39d5012ef)

`TamangVH1` and `TamangVH2` were added as cluster nodes using the Failover Cluster Manager GUI.

**Key actions:**
- Launched Failover Cluster Manager
- Ran cluster creation wizard
- Added both nodes by name

---

## Set Cluster Access Point and IP

![image](https://github.com/user-attachments/assets/e5779132-c927-428f-9d83-28300d3ce54e)
![image](https://github.com/user-attachments/assets/f3e6e23c-c230-4dcb-9e55-0fefaf3e0efd)

A cluster access point was created with the name `TamangCluster` and assigned a static IP for administration.

**Key actions:**
- Named cluster: `TamangCluster`  
- IP address: `192.168.0.200` (example placeholder)

---

## Add a Virtual Machine Role to the Cluster

![image](https://github.com/user-attachments/assets/fc9af4f5-65ea-4c9e-ad31-c65c31a68bcd)

Created a virtual machine role inside the cluster to provide high availability for application services.

**Key actions:**
- Navigated to Roles > Configure Role  
- Selected "Virtual Machine" as the high-availability role

---

## Check Cluster Disk Owner and Move for Testing

![image](https://github.com/user-attachments/assets/50e79d32-f22e-43d0-846c-57fc5cb90dcd)

Verified current cluster resource owner and moved the disk group to `TamangVH1` to simulate failover behavior.

**Key actions:**
```powershell
(Get-ClusterResource "Cluster Disk 1").OwnerNode
Move-ClusterGroup "Available Storage" -Node TamangVH1
```

---

## Create and Store VM Inside Cluster Node

![image](https://github.com/user-attachments/assets/703036a4-959c-4310-bcfd-1eaff065b40d)
![image](https://github.com/user-attachments/assets/9f1acc19-689d-4616-af93-ca55e5f9fa5a)

A VM was created using the Failover Cluster Manager to test VM-level high availability between both nodes.

**Key actions:**
- Used the wizard to create a new VM
- Specified name, generation, ISO path, and storage folder
- Completed VM wizard inside cluster scope

---

## Create Additional VM from TamangVH2 Node

![image](https://github.com/user-attachments/assets/94c8cffb-ea61-49e2-ad42-fd58e1e920d3)
![image](https://github.com/user-attachments/assets/0cdc8ff7-e9ed-4596-9149-d99f3a0e6430)

Used Hyper-V Manager on TamangVH2 to manually create a second virtual machine to include in the cluster.

**Key actions:**
- Chose local disk location and setup VM details
- Finished creation from the secondary node

---

## Assign VMs as Cluster Roles for High Availability

![image](https://github.com/user-attachments/assets/be3cceea-bd19-4155-8673-0a17119dc55a)
![image](https://github.com/user-attachments/assets/2336889c-dcf4-4fa8-abc5-edc44a31adc8)
![image](https://github.com/user-attachments/assets/b24c9952-4453-43aa-9c11-97b76915187b)

Configured both virtual machines (`VH-1` and `VH-2`) as high availability cluster roles. This ensures they can migrate automatically between `TamangVH1` and `TamangVH2`.

**Key actions:**
- Opened “Configure Role” in Failover Cluster Manager  
- Selected “Virtual Machine”  
- Chose both VMs and added them as HA roles  
- Verified both VMs show as “Running” and cluster-aware

---


## Perform Live Migration of VM for High Availability

![image](https://github.com/user-attachments/assets/38f4a324-b12e-410b-9ba7-90e8c5779083)
![image](https://github.com/user-attachments/assets/c888c1f1-5019-40df-9cff-48cca3b7246c)

A live migration of VM VH-2 was performed from TamangVH2 to TamangVH1 within the cluster. This demonstrates seamless failover capabilities without service interruption.

**Key actions:**
- Opened the Failover Cluster Manager
- Selected VM VH-2 and initiated "Live Migration"
- Chose TamangVH1 as the migration destination
- Confirmed successful transfer of VM role without reboot

---

## Final Cluster Overview

![image](https://github.com/user-attachments/assets/08c596fc-c0cb-453b-b15c-d1165acb7aec)

Both VMs (VH-1 and VH-2) are now configured as cluster roles and actively managed within the Failover Cluster Manager. This setup provides full redundancy and supports seamless failover in the event of host failure.

**Key actions:**
- Verified cluster roles display for both VMs
- Ensured both VMs are running and owned by separate nodes
- Confirmed successful completion of live migration and HA configuration

---


