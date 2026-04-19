<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Active Directory Logo"/>
</p>

# Active Directory Deployment in Azure (Lab 5)

---

## 🎯 Goals & Objectives

The goal of this project was to design and implement a functional Active Directory environment in a cloud setting while developing a deeper understanding of how core infrastructure components interact.

By the end of this lab, I aimed to:

- Deploy a Domain Controller in Microsoft Azure  
- Configure Active Directory Domain Services (AD DS)  
- Join a client machine to the domain  
- Create and manage users and Organizational Units  
- Implement and test security policies  
- Strengthen troubleshooting skills across DNS, networking, and system logs  
- Reflect on system behavior to improve future problem-solving approaches  

---

## 📌 Overview

This project demonstrates the deployment and configuration of an Active Directory Domain Services (AD DS) environment using Azure Virtual Machines. The setup simulates a real-world enterprise environment with centralized identity and access management.

More importantly, this lab served as a hands-on opportunity to connect theoretical knowledge with practical implementation, reinforcing how infrastructure, networking, and security concepts interdepend.

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
- Created Resource Group, Virtual Network, and two VMs  
- Configured Domain Controller with a **static private IP**  

![VM Setup](images/vm-setup.png)

---

### 2. DNS & Connectivity
- Configured Client-1 to use DC-1 as its DNS server  
- Verified connectivity using `ping` and `ipconfig /all`  

![DNS Config](images/dns-config.png)

---

### 3. Active Directory Deployment
- Installed AD DS and promoted DC-1 to a Domain Controller  
- Created domain: `mydomain.com`  

![AD Install](images/ad-install.png)

---

### 4. Directory Structure & Administration
- Created Organizational Units:
  - `_ADMINS`
  - `_EMPLOYEES`
  - `_CLIENTS`
- Created dedicated admin account (`jane_admin`)  

![OU Setup](images/ou-setup.png)

---

### 5. Domain Integration
- Joined Client-1 to the domain  
- Verified presence in Active Directory  
- Organized system within `_CLIENTS` OU  

![Domain Join](images/domain-join.png)

---

### 6. Scalable User Management
- Used PowerShell to create ~10,000 users  
- Verified proper placement within `_EMPLOYEES` OU  

![Users](images/users.png)

---

### 7. Security Policy Implementation
- Configured account lockout policy using Group Policy  
- Forced policy update (`gpupdate /force`)  
- Validated enforcement through failed login attempts  

---

### 8. Account Management & Logging
- Unlocked accounts and reset passwords  
- Disabled and re-enabled users  
- Reviewed authentication logs in Event Viewer  

![Logs](images/logs.png)

---

## 🔍 Troubleshooting & Problem-Solving

### DNS Dependency
- Issue: Domain join failure  
- Cause: Client using Azure default DNS  
- Resolution: Redirected DNS to Domain Controller  

---

### Network Configuration (Subnet Awareness)
- Issue: Systems unable to communicate  
- Cause: Misaligned network configuration  
- Resolution:
  - Verified both VMs were in the same VNet/subnet  
  - Corrected addressing  
  - Validated connectivity  

---

### Log Interpretation Challenge
- Issue: Difficulty identifying relevant events in logs  
- Observation:
  - Logs contain detailed but non-obvious information  
  - Requires filtering and contextual understanding  
- Insight:
  - Monitoring is not passive—it requires active interpretation  

---

## 🧠 Design Thinking

This lab reinforced intentional design choices:

- Static IP assignment ensures DNS stability  
- Organizational Units provide scalable structure  
- Separate admin accounts support least privilege principles  
- PowerShell enables efficient, large-scale operations  

These decisions reflect how systems are designed for maintainability and scalability in real environments.

---

## 🛡️ Security Perspective

- Simulated account lockouts through repeated failed logins  
- Observed how authentication attempts are logged  
- Identified how high log volume can obscure meaningful signals  

This highlights the importance of:
- Monitoring tools (SIEM)
- Alerting systems
- Structured log analysis  

---

## 🌍 Real-World Transfer

This experience extends beyond the lab environment:

- Cloud infrastructure can replicate traditional enterprise systems  
- Identity management is central to system security  
- Automation and policy enforcement are essential at scale  
- Monitoring and visibility are critical for operational security  

---

## 📌 Lessons Learned

- Active Directory is tightly coupled with DNS configuration  
- Network design (subnets, addressing) directly impacts system functionality  
- Logs require interpretation, not just observation  
- Troubleshooting is iterative and requires system-level thinking  
- Effective IT work combines technical skill with analytical reasoning  

---

## 💭 Reflection (Metacognitive Insight)

This lab shifted my understanding from simply executing steps to analyzing how systems behave.

Initially, I expected issues to be clearly visible and easy to diagnose. Instead, I found that many problems required deliberate investigation and a deeper understanding of system dependencies.

A key realization was that systems do not inherently highlight problems—meaningful signals must be identified within large volumes of data. This reinforced the importance of developing both technical skills and analytical thinking.

Moving forward, I will approach system configuration and troubleshooting with a stronger focus on:
- Anticipating dependencies  
- Verifying assumptions  
- Interpreting system feedback critically  

This shift from procedural execution to reflective problem-solving is essential for real-world IT work.
