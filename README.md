# Active Directory Home Lab (VirtualBox)

## Overview

This project documents the creation of a **virtual enterprise network environment** using **VirtualBox**. The lab simulates a corporate IT infrastructure with a **Windows Server Domain Controller** and a **Windows client workstation** to practice common IT support and system administration tasks.

The environment demonstrates key help desk responsibilities including:

- Active Directory user management
- Domain joining workstations
- Password resets and account unlocks
- Shared folder permissions
- Group Policy configuration
- Basic network troubleshooting

This lab was built to gain hands-on experience with tools commonly used in enterprise IT environments.

---

# Lab Architecture

The environment consists of a Windows Server domain controller and a Windows client connected through an isolated VirtualBox network.


<img width="521" height="311" alt="image" src="https://github.com/user-attachments/assets/d7b7c308-802b-4acd-8737-3fc17b4368b6" />


Services:
- Active Directory Domain Services
- DNS
- File Sharing
- Group Policy


---

# Environment Configuration

| Component | Configuration |
|----------|--------------|
| Hypervisor | VirtualBox |
| Server OS | Windows Server 2025 |
| Client OS | Windows 11 |
| Domain | corp.local |
| Server IP | 192.168.10.10 |
| Client IP | 192.168.10.20 |
| Network Type | Internal Network (LABNET) |

---

# Lab Objectives

The goals of this lab were to:

- Build a functional **Active Directory domain environment**
- Configure **DNS and domain services**
- Simulate **real-world help desk tasks**
- Practice **user and workstation administration**
- Document technical procedures and troubleshooting

---

# Step 1 — Virtual Machine Setup

Two virtual machines were created in VirtualBox.

### Domain Controller (CD11)

Configuration:

- 4 GB RAM  
- 2 CPU cores  
- 60 GB disk  
- Windows Server 2022 
- Static IP configuration
<img width="683" height="589" alt="image" src="https://github.com/user-attachments/assets/93322acc-adbd-448a-a76b-9ff451e52256" />
  

### Client Workstation (PC1)

Configuration:

- 4 GB RAM  
- 2 CPU cores  
- 50 GB disk  
- Windows 11
<img width="676" height="589" alt="image" src="https://github.com/user-attachments/assets/a565eb41-6c03-4bbc-9ae5-e93fdb49b0c1" />


Both VMs were connected to an **Internal Network named `LABNET`**.
<img width="776" height="511" alt="image" src="https://github.com/user-attachments/assets/a971610c-9e9b-4e68-ad4e-a01eb919bf7a" />
<img width="775" height="512" alt="image" src="https://github.com/user-attachments/assets/4d1abfc0-f9f3-49d3-a8ff-d89a1e2f0903" />



---

# Step 2 — Configure Server Networking

The domain controller was assigned a static IP address.

### Server IP Configuration


IP Address: 192.168.10.10
Subnet Mask: 255.255.255.0
DNS Server: 192.168.10.10


This server also functions as the **DNS server for the domain**.
<img width="1297" height="900" alt="image" src="https://github.com/user-attachments/assets/80de2856-c4b4-4256-a663-3c591608ec6f" />


---

# Step 3 — Install Active Directory Domain Services

Using **Server Manager**:

1. Add Roles and Features  
2. Install **Active Directory Domain Services**  
3. Promote server to Domain Controller  
4. Create new forest:


corp.local


After installation, the server rebooted and the domain environment became active.

<img width="1298" height="902" alt="image" src="https://github.com/user-attachments/assets/02a5152f-2f83-4bac-b9ff-4d35e8d6d12e" />


---

# Step 4 — Create Organizational Units and Users

To simulate a corporate environment, the following Organizational Units were created:

- Users
- Workstations
- IT
- Sales
<img width="1085" height="616" alt="image" src="https://github.com/user-attachments/assets/5a36652d-c8da-429a-9b77-33b7f0abd95f" />


Example user accounts were created:

| User | Username |
|-----|----------|
| Larry Bird | LBird |
| Mary Davis | MDavis |
| Zarah Manzi | ZManzi |

These accounts were used to test login, password reset, and permission management tasks.

<img width="1081" height="616" alt="image" src="https://github.com/user-attachments/assets/152ceca0-09fd-48d0-ab04-803ce050512f" />


---

# Step 5 — Join Client Workstation to Domain

The Windows client machine was configured with DNS pointing to the domain controller.

### Client Network Configuration


IP Address: 192.168.10.20
DNS Server: 192.168.10.10


The client was then joined to the domain:


corp.local

<img width="997" height="616" alt="image" src="https://github.com/user-attachments/assets/a7ff641f-e477-4c73-a279-cb818b02aad1" />



Domain login was verified using created user accounts.

---

## Step 6 — File Share and Permissions

A shared folder was created on the server to simulate a corporate file share.

Example network path:

`\\CD11\CompanyFiles`
<img width="496" height="328" alt="image" src="https://github.com/user-attachments/assets/313c8846-ac5a-43e2-a824-89cf66a82f56" />


Permissions were configured using:

- NTFS permissions
- Share permissions
- User and group access control

Access to the shared folder was verified from the client workstation.

---

## Step 7 — Group Policy Configuration

A **Group Policy Object (GPO)** was created and linked to the **Workstations OU**.
<img width="743" height="503" alt="image" src="https://github.com/user-attachments/assets/472021a2-1a9f-429a-a87f-954f6d4b0225" />


Example policy implemented:

- Desktop wallpaper enforcement

The policy was applied on the client machine using the following command:

`gpupdate /force`

Verification confirmed that the policy was successfully applied.
<img width="872" height="536" alt="image" src="https://github.com/user-attachments/assets/948088c2-ff1c-478b-b321-abb0a3b0fe81" />


---

## Troubleshooting

### Issue

The client workstation could not initially join the domain.

### Cause

The client DNS server was incorrectly set to a public DNS server instead of the domain controller.

### Resolution

The DNS configuration was corrected so that the client pointed to the domain controller.

Correct DNS configuration:

`DNS Server: 192.168.10.10`

After updating the DNS configuration, the workstation successfully joined the domain.

---

## Skills Demonstrated

- Active Directory administration
- Windows Server configuration
- DNS configuration
- Domain joining workstations
- User and group management
- NTFS and share permissions
- Group Policy management
- Virtualization with VirtualBox
- Network troubleshooting

---

## Tools and Technologies

- VirtualBox
- Windows Server 2022
- Windows 11
- Active Directory Domain Services
- DNS
- Group Policy
- Command-line tools such as `ping` and `nslookup`

---

## Future Improvements

Possible enhancements for this lab include:

- Implementing a **DHCP server**
- Adding additional client machines
- Deploying a **help desk ticketing system**
- Automating user creation with **PowerShell**
- Configuring **remote administration tools**

---


