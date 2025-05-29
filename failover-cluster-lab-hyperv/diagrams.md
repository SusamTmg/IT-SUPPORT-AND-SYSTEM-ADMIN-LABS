# Architecture Diagrams – Failover Cluster Lab

These diagrams provide a visual breakdown of the enterprise-grade high availability infrastructure simulated in this lab using Hyper-V, Active Directory, iSCSI storage, and Windows Failover Clustering. Both diagrams represent different aspects of the system: the architecture layout and the failover mechanism.

---

## Failover Cluster System Architecture with IP Addresses

![Image](https://github.com/user-attachments/assets/e1f67b19-1d36-4fba-9753-2371b4182e8c)

This diagram shows the full system topology of the virtual lab setup. It illustrates how each component is logically and physically interconnected within the network using distinct subnets for redundancy and isolation.

### 🔍 What This Diagram Shows:
- **TamangVH1** and **TamangVH2** are the two Hyper-V failover cluster nodes responsible for running virtual machines.
- A dedicated **Domain Controller (TamangDC)** handles domain authentication, DNS, and joins all nodes to the `tamang.local` domain.
- **TamangStorage** acts as an iSCSI target server, providing shared VHDX disks accessed by the cluster nodes.
- Three separate networks ensure performance and failover reliability:
  - **Public Network (172.50.39.x)** – for domain join, AD, and general network communication.
  - **Storage Network (192.168.111.x)** – for iSCSI storage access.
  - **Heartbeat Network (192.168.222.x)** – for health monitoring and failover detection between nodes.
- The **TamangCluster** object manages the cluster at IP `172.50.39.150`.
- **TamangAppServer**, the VM hosted inside the cluster, benefits from live migration and high availability.

This architecture represents real-world enterprise systems that require uptime, performance, and fault tolerance.

---

## Failover Role Migration Flow

![Image](https://github.com/user-attachments/assets/0d679b9a-430f-40d6-8348-166235b244c6)

This diagram visually explains what happens when one of the Hyper-V cluster nodes fails. It demonstrates the automated failover process that maintains continuous service availability.

### 🔍 What This Diagram Shows:
- The cluster initially runs VM roles (e.g., `VM1`, `VM2`) on **TamangVH1**.
- When **TamangVH1** becomes unavailable (e.g., due to hardware failure or maintenance), the **heartbeat signal is lost**.
- The cluster detects the failure and immediately shifts control to **TamangVH2**.
- **TamangVH2** then:
  - Takes ownership of the VM roles
  - Connects to the same shared iSCSI VHDX disks
  - Starts running the VMs without downtime
- This process ensures the end-user or service experience remains uninterrupted.

The diagram simulates how real businesses use failover clustering for disaster recovery, uptime SLAs, and virtual server continuity.

---

