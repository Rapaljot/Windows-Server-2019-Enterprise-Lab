# Windows Server 2019 Enterprise Home Lab
## Overview

This project is a hands-on Windows Server 2025 home lab designed to simulate
a small business IT environment.

The purpose of this lab is to develop practical experience with Windows Server
administration, Active Directory, networking, Group Policy, user management,
file permissions, PowerShell, and common IT support tasks.

The environment is built using virtual machines in VMware Workstation.

---

## Project Objectives

The main objectives of this project are to gain hands-on experience with:

- Windows Server 2019
- Active Directory Domain Services (AD DS)
- Domain Controllers
- DNS
- DHCP
- Group Policy
- Organizational Units (OUs)
- Active Directory users and groups
- Windows domain joins
- NTFS permissions
- Shared folders
- PowerShell administration
- Server troubleshooting
- Windows client support
- Basic enterprise IT administration

---

## Lab Environment

The lab is hosted using VMware Workstation.

### Technologies Used

- VMware Workstation
- Windows Server 2019
- Windows client operating system
- Active Directory Domain Services
- DNS
- DHCP
- Group Policy Management
- PowerShell
- Windows Server Manager

---

## Lab Architecture

The environment is designed to simulate a small business network.

### Servers

| Hostname | Operating System | Purpose |
|----------|------------------|---------|
| DC01 | Windows Server 2025 | Primary Domain Controller |
| DC02 | Windows Server 2025 | Secondary Domain Controller |

### Client Computers

| Hostname | Operating System | Purpose |
|----------|------------------|---------|
| CLIENT01 | Windows | Domain-joined workstation |

More client machines may be added as the lab expands.

---

## Domain Configuration

The Active Directory environment will include:

- Active Directory Domain Services
- DNS
- DHCP
- Organizational Units
- User accounts
- Security groups
- Group Policies
- Domain-joined client computers

### Domain Name

`rapaljotlab.local`

---

## Organizational Unit Structure

The Active Directory environment will be organized into departments similar
to a real company.

```text
RapaljotLab
│
├── Users
│   ├── HR
│   ├── Finance
│   ├── Sales
│   └── IT
│
├── Computers
│
├── Servers
│
└── Groups