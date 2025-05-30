# Failover Cluster & Virtualization Lab (Hyper-V + iSCSI + Windows Server)

This project simulates a **production-grade high availability infrastructure** for a company’s HR department. It uses **Hyper-V**, **Windows Server**, **Active Directory**, **iSCSI (Internet Small Computer System Interface) shared storage**, and **Windows Failover Clustering** to build a resilient and redundant virtual environment.

---

## Project Objective

> To simulate a highly available enterprise environment with failover capabilities and shared storage to support business-critical services like an HR application server.

---

## What I Built

| Component | Purpose |
|----------|---------|
| **TamangDC (Domain Controller)** | Manages AD, DNS, domain authentication |
| **TamangStorage (iSCSI Server)** | Provides shared VHDX disks via iSCSI |
| **TamangVH1 & TamangVH2 (Cluster Nodes)** | Hosts VMs with failover and live migration |
| **HR App VM (Clustered Role)** | Runs critical services with redundancy |

---

## Configuration Highlights

### Hyper-V & Networking
- Created 3 virtual switches: Public, Storage, and Heartbeat
- Assigned static IPs for each subnet
- Automated VM setup using PowerShell

### Active Directory
- Installed and promoted TamangDC as `tamang.local`
- Joined all nodes to the domain

### iSCSI Shared Storage
- Created VHDX disks on TamangStorage
- Configured secure iSCSI targets/initiators
- Mapped disks to both VH1 and VH2 nodes

### Failover Clustering
- Installed Failover Clustering feature
- Created a 2-node cluster with TamangVH1 & VH2
- Configured clustered VMs and enabled live migration
- Tested failover by simulating node failure

---

## Skills Demonstrated

| Area | Skills |
|------|--------|
| **Virtualization** | Hyper-V, nested VM deployment |
| **Networking** | Multi-subnet configuration, IP planning |
| **PowerShell** | VM creation, NIC and IP automation |
| **Windows Server** | AD DS, DNS, Failover Clustering, iSCSI Target |
| **Storage Management** | VHDX disk provisioning, iSCSI connectivity |
| **High Availability** | Live migration, redundancy testing |

---

## Screenshots

Screenshots are organized under `/screenshots.md`.  
They include:
- IP schema and network plan
- iSCSI target configuration
- Domain Controller promotion
- Failover Cluster validation
- Live migration demo

---

## Folder Structure

```bash
failover-cluster-lab-hyperv/
│
├── README.md
├── Architecture Diagrams.md/
├── Lab-screenshots.md/
│  

