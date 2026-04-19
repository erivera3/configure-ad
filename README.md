<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Active Directory Logo"/>
</p>

# Active Directory Deployment in Azure (Lab 5)

---

## 🎯 Goals & Objectives

The goal of this project was to build a functional Active Directory environment in a cloud setting and understand how core IT infrastructure components interact.

By the end of this lab, I aimed to:

- Deploy a Domain Controller in Microsoft Azure
- Configure Active Directory Domain Services (AD DS)
- Join a client machine to the domain
- Create and manage users and Organizational Units
- Implement and test security policies (account lockout)
- Validate authentication and system behavior
- Develop troubleshooting skills across networking, DNS, and system logs

---

## 📌 Overview

This project demonstrates the deployment and configuration of an Active Directory Domain Services (AD DS) environment using Azure Virtual Machines. A Domain Controller and client machine were configured to simulate a real-world enterprise setup with centralized identity and access management.

---

## 🧰 Technologies Used

- Microsoft Azure (Virtual Machines)
- Active Directory Domain Services (AD DS)
- Remote Desktop Protocol (RDP)
- PowerShell (ISE)
- Group Policy Management
- DNS

---

## 💻 Environment

- Windows Server 2022 (Domain Controller: DC-1)
- Windows 10 (Client Machine: Client-1)
- Domain: `mydomain.com`
- Azure Virtual Network (VNet)

---

## ⚙️ Implementation

### 1. Infrastructure Setup
- Created Resource Group, Virtual Network, and two VMs (DC-1, Client-1)
- Configured Domain Controller with a **static private IP**

![VM Setup](images/vm-setup.png)

---

### 2. DNS & Connectivity
- Configured Client-1 to use DC-1 as its DNS server
- Verified connectivity using:
  - `ping`
  - `ipconfig /all`

![DNS Config](images/dns-config.png)

---

### 3. Active Directory Deployment
- Installed AD DS on DC-1
- Promoted server to Domain Controller
- Created domain: `mydomain.com`

![AD Install](images/ad-install.png)

---

### 4. Directory Structure & Admin Setup
- Created Organizational Units:
  - `_ADMINS`
  - `_EMPLOYEES`
  - `_CLIENTS`
- Created admin account: `jane_admin`
- Assigned to Domain Admins group

![OU Setup](images/ou-setup.png)

---

### 5. Domain Join
- Joined Client-1 to the domain
- Verified presence in Active Directory
- Organized into `_CLIENTS` OU

![Domain Join](images/domain-join.png)

---

### 6. User Management at Scale
- Used PowerShell to generate ~10,000 user accounts
- Verified accounts in `_EMPLOYEES` OU

![Users](images/users.png)

---

### 7. Security Policy Implementation
- Configured account lockout policy via Group Policy
- Forced policy update using `gpupdate /force`
- Triggered lockouts through repeated failed logins

---

### 8. Account Management & Logging
- Unlocked accounts and reset passwords
- Disabled and re-enabled users
- Reviewed authentication activity using Event Viewer

![Logs](images/logs.png)

---

## 🔍 Troubleshooting

### DNS Misconfiguration
- Issue: Client unable to join domain  
- Cause: Using Azure default DNS  
- Fix: Pointed DNS to Domain Controller private IP  

---

### Network / Subnet Misconfiguration
- Issue: Systems could not communicate  
- Cause: Incorrect network/subnet alignment  
- Fix:
  - Verified both VMs in same VNet/subnet
  - Corrected configuration
  - Confirmed connectivity with ping  

---

### Log Analysis Challenge
- Issue: Difficulty identifying relevant events in logs  
- Cause: High volume of detailed entries with no obvious flags  
- Insight:
  - Logs require filtering and interpretation
  - Important events can be missed without context or monitoring tools  

---

## 🧠 Design Decisions

- Assigned a **static IP** to the Domain Controller to maintain DNS consistency  
- Created separate admin account instead of using default administrator  
- Structured Organizational Units to reflect real-world environments  
- Used PowerShell for scalable user creation  

---

## 🛡️ Security Perspective

- Simulated account lockout through repeated failed login attempts  
- Observed how authentication events are recorded in logs  
- Identified how lack of monitoring could delay detection of suspicious behavior  

---

## 🌍 Real-World Relevance

In production environments:

- User provisioning is automated through HR systems  
- Logs are aggregated into SIEM platforms (e.g., Microsoft Sentinel)  
- Group Policy enforces organization-wide security standards  
- Monitoring and alerting are automated  

---

## ✅ Results

- Successfully deployed Active Directory in Azure  
- Configured DNS and verified domain communication  
- Created and managed users and OUs  
- Joined client machine to domain  
- Implemented and tested security policies  
- Verified authentication and logging behavior  

---

## 📌 Lessons Learned

- Active Directory is highly dependent on DNS configuration  
- Network misconfiguration (subnets, DNS) can break communication silently  
- Logs require analysis and context, not just observation  
- Troubleshooting is a critical skill in IT environments  
- Security visibility depends on proper monitoring tools  

---

## 💭 Personal Reflection

This project changed how I view IT systems.

Initially, I assumed that system issues would be clearly visible and easy to identify. In practice, I found that many problems (DNS misconfiguration, subnet issues, log analysis) required deliberate investigation and understanding of how systems interact.

One key realization was how easy it is for issues—or even suspicious behavior—to go unnoticed without proper monitoring. Logs contain the necessary information, but identifying meaningful events requires both experience and the right tools.

This experience reinforced the importance of:
- Understanding system dependencies (DNS, networking, authentication)
- Developing strong troubleshooting skills
- Recognizing the role of monitoring and security tools in real environments
