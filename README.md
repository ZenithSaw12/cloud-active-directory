# Cloud Identity & Security Monitoring Lab: Microsoft Azure & Active Directory

## 🎯 Project Objective
This lab demonstrates the deployment, configuration, and monitoring of a cloud-based **Hybrid Identity Environment**. By utilizing **Microsoft Azure**, **Windows Server**, and **Active Directory Domain Services (AD DS)**, I established a secure corporate network architecture. The primary focus was on user lifecycle management, Role-Based Access Control (RBAC), and analyzing security telemetry via the Windows Event Viewer to simulate a SOC Analyst's investigation workflow.

---

## 🏗️ Cloud Infrastructure (Microsoft Azure)

### Resource Management
All resources were organized within a centralized Resource Group (AD-Lab) to ensure administrative efficiency. I implemented **Cloud Governance** by configuring an **Auto-shutdown policy** (11:00 PM EST) for all virtual assets to optimize costs and follow sustainability best practices.

> Resource Group
>
> <img src="images/resource-group.png" alt="Resource Group Overview" width="60%">

> Auto-Shutdown Policy
> 
> ![Auto-shutdown Policy](images/auto-shutdown.png)

### Network Security & Topology
The environment consists of two virtual machines: a Domain Controller (DC01) and a Client Workstation (Client01). Traffic is filtered through **Network Security Groups (NSGs)** to maintain a hardened perimeter, allowing only necessary traffic for management and domain operations.

> Network Topology Diagram
>
> <img src="images/AD-Lab.png" alt="Network Topology" width="50%">

> Network Security Group Inbound Rules
>
> <img src="images/client-sec-rules.png" alt="NSG Inbound Rules" width="60%">

---

## 🛠️ Active Directory Configuration

### Domain Services Deployment
I provisioned a Windows Server instance as the **Domain Controller** for the `corp.local` forest. This involved the installation of AD DS and the configuration of internal DNS to handle domain-wide name resolution.

> AD DS Installation
> 
> <img src="images/adds.png" alt="AD DS Screenshot" width="60%">

> Configuring Forest/ Promoting to Domain Controller
>
> <img src="images/forest.png" alt="Forest Screenshot" width="60%">

> Domain Properties
>
> <img src="images/dc-props.png" alt="Domain Properties Screenshot" width="60%">

> AD DS Verification
>
> <img src="images/corp.local.png" alt="AC Overview Screenshot" width="60%">


### User Management & Role Based Access Control
I created an **Organizational Unit (OU)** structure to logically segment users. To simulate real-world identity management, I provisioned test accounts and implemented **Role-Based Access Control (RBAC)** by managing permissions through Security Groups.

* **Users:** Alice, Bob, and Charlie.
* **Provisioning:** Accounts created with standard corporate password policies.
* **Access Control:** Manually configured the "Remote Desktop Users" group to allow the `alice` account remote access to the workstation.

> User Creation
>
> <img src="images/create-users.png" alt="User Alice Creation Screenshot" width="60%">

> User Inventory
>
> <img src="images/more-users.png" alt="User Inventory Screenshot" width="60%">

> Alice Password Reset
>
> <img src="images/reset-password.png" alt="Resetting Alice's Password Screenshot" width="60%">

> Configuring Remote Desktop Access For Alice
>
> <img src="images/addUserToRemote.png" alt="Adding User to Remote Desktop Screenshot" width="60%">


---

## 🧪 Testing & Verification

### Domain Integration
The Client VM was successfully joined to the `corp.local` domain. Connection was verified using `ping` and `nslookup` to ensure proper communication between the workstation and the DC.

> Join Client Machine to Domain
>
> <img src="images/join-domain.png" alt="Domain Join Screenshot" width="60%">

### Authentication & Access
Verified the "Alice" account's ability to log in to the domain environment and access shared network resources. I utilized the `whoami` command to confirm that the identity session was correctly established as `corp\alice`.

> Joining Alice to `corp.local`
>
> <img src="images/aliceDomain.png" alt="Joining Alice to Domain Screenshot" width="50%">

> Veryify Domain Access
>
> <img src="images/pingDC.png" alt="Pinging DC from Alice Screenshot" width="50%">

> Shared Folder Access From Alice Account
>
> <img src="images/shared-folders.png" alt="Shared Folders Access Screenshot" width="60%">


---

## 🛡️ Security Monitoring (SOC Perspective)

A key objective of this lab was identifying and correlating security events within the **Windows Event Viewer**. This simulates the telemetry analysis performed by SOC analysts during incident response.

### Event Correlation Table
| Action Performed | Event ID | SOC Relevance |
| :--- | :--- | :--- |
| **New Account Creation** | 4720 | Tracking user provisioning for auditing. |
| **Successful Logon** | 4624 | Baseline for normal user activity. |
| **Password Reset (Admin)** | 4724 | Detecting potential unauthorized credential changes. |
| **Privilege Assignment** | 4672 | Monitoring for administrative "SuperUser" logins. |

> Event Viewer
>
> <img src="images/event-viewer.png" alt="Event Viewer Screenshot" width="60%">

---

## 🚀 Skills & Tools Demonstrated
* **Cloud Platform:** Microsoft Azure (VNets, NSGs, Resource Groups, FinOps Governance).
* **Identity Management:** Active Directory Domain Services (AD DS), OU Design, User Lifecycle Management.
* **Networking:** DNS Configuration, DHCP, CIDR Subnetting, Troubleshooting (Ping, Nslookup).
* **Security & Compliance:** Role-Based Access Control (RBAC), Least Privilege Principle, NIST CSF/CIS Control Mapping.
* **Telemetry:** Windows Event Log analysis and security event correlation.
