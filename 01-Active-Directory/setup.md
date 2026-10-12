# Active Directory Setup

## Overview

For this part of the project, I set up a Windows Server 2025 Domain Controller for Kareem Industries. The goal was to create a working Active Directory environment where I could manage users, computers, security groups, and permissions from one server.

I also connected a Windows 11 workstation to the domain to test authentication and access to network resources.

## Lab Setup

| Device | OS | IP Address |
|---|---|---|
| KI-DC01 | Windows Server 2025 | 192.168.50.10 |
| KI-PC01 | Windows 11 | 192.168.50.20 |

- **Domain:** `ad.kareemindustries.test`
- **Virtualization:** Oracle VirtualBox
- **Network:** `192.168.50.0/24`

## 1. Setting Up Active Directory

I installed Windows Server 2025, configured the server's IP address, installed the Active Directory Domain Services (AD DS) role, and promoted the server to a Domain Controller.

After setting up the domain, I used Active Directory Users and Computers (ADUC) to create and manage the company's users and groups.

## 2. Organizational Units

I created the following OUs to organize the environment:

- KI-Users (HR, IT, Finance, Sales, Management)
- KI-Groups
- KI-Workstations

This keeps user accounts, security groups, and computers organized instead of leaving everything in the default containers. It also makes it easier to apply Group Policy to specific departments or devices.

## 3. Users and Security Groups

I created two test accounts:

| Username | Name | Role |
|---|---|---|
| mmohamed | Mira Mohamed | HR employee |
| jdoe | John Doe | Test user outside HR |

For file permissions, I used the **AGDLP model**:

`Accounts → Global Groups → Domain Local Groups → Permissions`

For example:

`mmohamed → SG-HR → DomainLocal-HR-Modify → HR Confidential`

Instead of assigning folder permissions directly to each employee, I can manage access through group membership.

I tested this by logging into the domain workstation with both accounts. The HR account could access and modify files in the shared folder, while the unauthorized account received an access-denied message.

## 4. Joining Windows 11 to the Domain

I installed Windows 11 on KI-PC01 and joined it to `ad.kareemindustries.test`.

After joining, I checked ADUC and confirmed that KI-PC01 appeared as a computer object. I then moved it into the KI-Workstations OU for Group Policy management.

I also tested domain login using the accounts created earlier.

## 5. PowerShell Commands Used

**List Active Directory users and account status:**

```powershell
Get-ADUser -Filter * | Select-Object Name, SamAccountName, Enabled
```

**Check members of the HR security group:**

```powershell
Get-ADGroupMember -Identity "SG-HR"
```

**Check the domain-local group:**

```powershell
Get-ADGroupMember -Identity "DomainLocal-HR-Modify"
```

The results confirmed that `mmohamed` was a member of `SG-HR`, and `SG-HR` was nested inside `DomainLocal-HR-Modify`.

## 6. Issues I Ran Into

One issue I encountered was accessing the HR Confidential share from KI-PC01.

Initially, Windows couldn't locate the server using the hostname I entered. I tested connectivity to the Domain Controller by IP address and confirmed that SMB port 445 was reachable.

After checking DNS records, I realized I was using the wrong server hostname. The correct hostname was `KI-DC01`, not `KI-AD`.

Once I corrected the UNC path, the workstation could reach the share.

I also ran into an issue where `Get-ADUser` wasn't recognized because I was using Command Prompt instead of PowerShell. Switching to PowerShell and importing the Active Directory module resolved it.

## 7. What I Learned

This part of the lab helped me get more comfortable with Active Directory administration, especially how users, OUs, and security groups work together.

The biggest takeaway was understanding how group-based permissions work in practice. Instead of just configuring permissions, I tested them using different accounts to make sure authorized users had access and unauthorized users didn't.

I also got more practice troubleshooting DNS and network connectivity rather than immediately changing settings when something wasn't working.

---

**Status:** Completed initial AD setup and verification. Additional configurations and documentation are ongoing.
