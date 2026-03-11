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
- Windows Server 2025  
- Static IP configuration  

### Client Workstation (PC1)

Configuration:

- 4 GB RAM  
- 2 CPU cores  
- 50 GB disk  
- Windows 11  

Both VMs were connected to an **Internal Network named `LABNET`**.

---

# Step 2 — Configure Server Networking

The domain controller was assigned a static IP address.

### Server IP Configuration


IP Address: 192.168.10.10
Subnet Mask: 255.255.255.0
DNS Server: 192.168.10.10


This server also functions as the **DNS server for the domain**.

---

# Step 3 — Install Active Directory Domain Services

Using **Server Manager**:

1. Add Roles and Features  
2. Install **Active Directory Domain Services**  
3. Promote server to Domain Controller  
4. Create new forest:


corp.local


After installation, the server rebooted and the domain environment became active.

---

# Step 4 — Create Organizational Units and Users

To simulate a corporate environment, the following Organizational Units were created:

- Users
- Workstations
- IT
- Sales

Example user accounts were created:

| User | Username |
|-----|----------|
| Larry Bird | LBird |
| Mary Davis | MDavis |
| Zarah Manzi | ZManzi |

These accounts were used to test login, password reset, and permission management tasks.

---

# Step 5 — Join Client Workstation to Domain

The Windows client machine was configured with DNS pointing to the domain controller.

### Client Network Configuration


IP Address: 192.168.10.20
DNS Server: 192.168.10.10


The client was then joined to the domain:


corp.local


Domain login was verified using created user accounts.

---

## Step 6 — File Share and Permissions

A shared folder was created on the server to simulate a corporate file share.

Example network path:

`\\DC1\CompanyFiles`

Permissions were configured using:

- NTFS permissions
- Share permissions
- User and group access control

Access to the shared folder was verified from the client workstation.

---

## Step 7 — Group Policy Configuration

A **Group Policy Object (GPO)** was created and linked to the **Workstations OU**.

Example policy implemented:

- Desktop wallpaper enforcement

The policy was applied on the client machine using the following command:

`gpupdate /force`

Verification confirmed that the policy was successfully applied.

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

## Screenshots

Example screenshots included in this repository:

- VirtualBox network configuration
- Windows Server installation
- Active Directory domain creation
- User account management
- Successful domain login
- Group Policy application

Screenshots are stored in the **/screenshots** folder.

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
- Windows Server 2025
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


