# Kareem Industries — IT Infrastructure Home Lab

**Windows Server 2025 | Active Directory | Group Policy | Windows 11 | PowerShell | DNS | SMB**

A virtualized enterprise IT environment built to demonstrate practical Windows systems administration, identity management, endpoint security, and network troubleshooting skills.

## Project Overview

Kareem Industries is a fictional company infrastructure project developed using Oracle VirtualBox. The lab simulates core IT operations performed by Help Desk Tier II and Junior Systems Administrators, with an emphasis on deploying, configuring, securing, troubleshooting, and validating Windows-based infrastructure.

The project is being developed in phases, with additional capabilities and technical documentation added as configurations are tested.

## Lab Environment

| Hostname | Operating System / Role | IPv4 Address |
|---|---|---|
| KI-DC01 | Windows Server 2025 — Domain Controller | 192.168.50.10 |
| KI-PC01 | Windows 11 — Domain-Joined Workstation | 192.168.50.20 |

- **Active Directory Domain:** `ad.kareemindustries.test`
- **Hypervisor:** Oracle VirtualBox
- **Internal Lab Subnet:** `192.168.50.0/24`
- **Domain Services:** Active Directory Domain Services (AD DS), DNS

## Implemented Infrastructure

### 1. Active Directory & Identity Management
- Deployed and configured an Active Directory Domain Controller.
- Created departmental Organizational Units (OUs) for HR, IT, Finance, Sales, and Management.
- Provisioned domain user accounts and security groups.
- Joined KI-PC01 to the Active Directory domain.
- Implemented the AGDLP security group nesting model to simplify permission management.
- Verified domain user accounts and group membership using PowerShell.

### 2. File Sharing & Access Control
- Configured an SMB network share for confidential HR files.
- Applied NTFS and share permissions using Active Directory security groups.
- Validated authorized read/write access with an HR account.
- Tested unauthorized access using a separate domain account and confirmed access was denied.
- Implemented group-based permissions rather than assigning individual user permissions.

### 3. Group Policy & Endpoint Security
- Created a dedicated workstation OU and linked a custom security GPO.
- Configured an inactivity timeout of 600 seconds (10 minutes).
- Forced Group Policy refresh using `gpupdate /force`.
- Verified GPO application using `gpresult /r`.
- Confirmed the configured inactivity timeout through PowerShell.

### 4. Networking & DNS Troubleshooting
- Configured static IPv4 addressing for the internal lab network.
- Validated network connectivity between the workstation and Domain Controller using ICMP.
- Verified SMB service reachability over TCP port 445.
- Investigated hostname resolution failures using `nslookup`.
- Corrected a hostname reference issue and successfully accessed the intended SMB share.
- Verified Active Directory DNS records through DNS Manager.

### 5. PowerShell Administration
Used PowerShell to perform administrative verification and auditing tasks, including:

- Enumerating Active Directory users and account status.
- Inspecting nested security group membership.
- Validating domain authentication and current user identity.
- Verifying Group Policy application.
- Testing network connectivity and DNS resolution.

## Troubleshooting Experience

During deployment, several issues required hands-on investigation:

| Issue | Troubleshooting / Resolution |
|---|---|
| Network share inaccessible | Tested IP connectivity, SMB port reachability, and DNS resolution |
| Hostname resolution failure | Inspected DNS records and corrected the server hostname reference |
| Unauthorized file access | Verified that a non-HR account was denied access |
| Group Policy verification required elevation | Used an elevated PowerShell session to inspect computer policy results |
| Active Directory PowerShell command unrecognized | Switched from Command Prompt to PowerShell and imported the Active Directory module |

## Planned Enhancements

- PowerShell automation and administrative reporting
- Windows Server backup and recovery testing
- Event log monitoring and system administration
- Additional Group Policy security configurations
- Infrastructure diagrams and configuration screenshots
- Expanded troubleshooting documentation

## Project Documentation

Detailed configuration procedures, validation screenshots, and troubleshooting notes will be added as the project develops.

## Project Objective

Develop and demonstrate hands-on experience with enterprise Windows infrastructure, Active Directory administration, access control, endpoint management, and structured troubleshooting.

The goal is to build a documented technical portfolio that reflects practical responsibilities encountered in a real life Systems Administrator role.

---

**Project Status:** Phase 1 — In Progress

**Environment:** Virtualized educational lab using fictional organizational identities and infrastructure.
