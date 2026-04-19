<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Active Directory Logo"/>
</p>

<h1>Active Directory Deployment in Azure (Lab 5)</h1>

<p>
This lab demonstrates the deployment of an on-premises style <b>Active Directory Domain Services (AD DS)</b> environment using Microsoft Azure Virtual Machines. The environment includes a Domain Controller and a domain-joined client machine with user and policy management.
</p>

---

<h2>🎯 Objective</h2>
<p>
Deploy and configure Active Directory in Azure, create users and organizational units, join a client machine to the domain, and implement account security policies.
</p>

---

<h2>🧰 Technologies Used</h2>

<ul>
  <li>Microsoft Azure (Virtual Machines)</li>
  <li>Active Directory Domain Services (AD DS)</li>
  <li>Remote Desktop Protocol (RDP)</li>
  <li>PowerShell (ISE)</li>
  <li>Group Policy Management</li>
</ul>

---

<h2>💻 Operating Systems</h2>

<ul>
  <li>Windows Server 2022 (Domain Controller)</li>
  <li>Windows 10 (Client Machine)</li>
</ul>

---

<h2>🧱 Architecture</h2>

<ul>
  <li>Domain Controller: DC-1</li>
  <li>Client Machine: Client-1</li>
  <li>Domain: mydomain.com</li>
  <li>Azure Virtual Network for internal communication</li>
</ul>

---

<h2>⚙️ Deployment Process</h2>

<h3>Step 1: Build Azure Infrastructure</h3>
<p>
Created a Resource Group, Virtual Network, and two Virtual Machines (DC-1 and Client-1). Both machines were placed in the same network to allow communication.
</p>

<p align="center">
  <img src="YOUR_IMAGE_1.png"/>
</p>

<p>
Configured the Domain Controller with a <b>static private IP</b> to prevent DNS issues caused by IP changes. :contentReference[oaicite:0]{index=0}
</p>

---

<h3>Step 2: Configure DNS and Connectivity</h3>
<p>
Updated Client-1’s DNS settings to point to the Domain Controller’s private IP address. Verified connectivity using <b>ping</b> and <b>ipconfig /all</b>.
</p>

<p align="center">
  <img src="YOUR_IMAGE_2.png"/>
</p>

---

<h3>Step 3: Install Active Directory Domain Services</h3>
<p>
Installed AD DS on DC-1 and promoted it to a Domain Controller by creating a new forest (<b>mydomain.com</b>). :contentReference[oaicite:1]{index=1}
</p>

<p align="center">
  <img src="YOUR_IMAGE_3.png"/>
</p>

---

<h3>Step 4: Create Organizational Units and Admin User</h3>
<p>
Created Organizational Units (<b>_EMPLOYEES</b>, <b>_ADMINS</b>) and a domain admin account (<b>jane_admin</b>). Added the account to the Domain Admins group.
</p>

<p align="center">
  <img src="YOUR_IMAGE_4.png"/>
</p>

---

<h3>Step 5: Join Client Machine to Domain</h3>
<p>
Joined Client-1 to the domain and verified it appeared in Active Directory. Moved the machine into the <b>_CLIENTS</b> OU.
</p>

<p align="center">
  <img src="YOUR_IMAGE_5.png"/>
</p>

---

<h3>Step 6: Enable Remote Desktop Access</h3>
<p>
Configured Client-1 to allow domain users to access Remote Desktop.
</p>

<p align="center">
  <img src="YOUR_IMAGE_6.png"/>
</p>

---

<h3>Step 7: Bulk User Creation with PowerShell</h3>
<p>
Used PowerShell ISE to run a script that generated <b>10,000 user accounts</b> for testing within Active Directory.
</p>

<p align="center">
  <img src="YOUR_IMAGE_7.png"/>
</p>

---

<h3>Step 8: Test Authentication</h3>
<p>
Logged into Client-1 using one of the newly created domain users to verify authentication worked correctly. :contentReference[oaicite:2]{index=2}
</p>

---

<h3>Step 9: Configure Account Lockout Policy</h3>
<p>
Configured Group Policy to lock accounts after multiple failed login attempts. Forced policy update using <b>gpupdate /force</b> and verified results.
</p>

---

<h3>Step 10: Unlock and Manage Accounts</h3>
<p>
Tested account lockouts, unlocked accounts in Active Directory, reset passwords, and verified login functionality.
</p>

<p align="center">
  <img src="YOUR_IMAGE_8.png"/>
</p>

---

<h3>Step 11: Disable/Enable Accounts & Review Logs</h3>
<p>
Disabled and re-enabled accounts to observe behavior. Checked security logs using <b>Event Viewer</b> to track login attempts and account activity.
</p>

<p align="center">
  <img src="YOUR_IMAGE_9.png"/>
</p>

---

<h2>✅ Results</h2>

<ul>
  <li>Successfully deployed Active Directory in Azure</li>
  <li>Configured DNS for domain communication</li>
  <li>Created and managed users and OUs</li>
  <li>Joined client machine to domain</li>
  <li>Implemented account lockout security policy</li>
  <li>Verified authentication and logging</li>
</ul>

---

<h2>📌 Key Takeaways</h2>

<ul>
  <li>DNS configuration is critical for Active Directory functionality</li>
  <li>Static IP assignment prevents domain resolution failures</li>
  <li>Group Policy is essential for enforcing security controls</li>
  <li>PowerShell enables scalable user management</li>
  <li>Event logs provide visibility into authentication activity</li>
</ul>
