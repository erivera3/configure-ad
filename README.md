<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Active Directory Logo"/>
</p>

<h1>Active Directory Deployment in Azure (Lab 5)</h1>

<p>
This lab demonstrates the deployment and configuration of an Active Directory Domain Services (AD DS) environment in Microsoft Azure. A Domain Controller and client machine were configured to simulate a basic enterprise network with centralized authentication, user management, and security policy enforcement.
</p>

---

<h2>🎯 Objective</h2>
<p>
Deploy a functional Active Directory environment in Azure, join a client machine to the domain, and implement user management and security controls.
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

<h3>Step 1: Azure Infrastructure Deployment</h3>
<p>
Provisioned a Resource Group, Virtual Network, and two virtual machines (DC-1 and Client-1) within the same network to enable internal communication.
</p>

<p align="center">
  <img src="YOUR_IMAGE_1.png"/>
</p>

<p>
Configured the Domain Controller with a static private IP address to prevent DNS failures caused by dynamic IP changes.
</p>

---

<h3>Step 2: Network Connectivity and DNS Configuration</h3>
<p>
Configured the client machine to use the Domain Controller’s private IP address as its DNS server. Verified connectivity by successfully pinging the Domain Controller and confirming DNS settings using <b>ipconfig /all</b>.
</p>

<p align="center">
  <img src="YOUR_IMAGE_2.png"/>
</p>

---

<h3>Step 3: Active Directory Installation and Domain Setup</h3>
<p>
Installed Active Directory Domain Services on the Domain Controller and promoted it to a Domain Controller by creating a new forest (<b>mydomain.com</b>). Verified successful deployment by logging in using domain credentials.
</p>

<p align="center">
  <img src="YOUR_IMAGE_3.png"/>
</p>

---

<h3>Step 4: Organizational Units and Administrative Account</h3>
<p>
Created Organizational Units (<b>_EMPLOYEES</b>, <b>_ADMINS</b>) to organize users and administrative roles. Created a dedicated domain admin account (<b>jane_admin</b>) and added it to the Domain Admins group.
</p>

<p align="center">
  <img src="YOUR_IMAGE_4.png"/>
</p>

---

<h3>Step 5: Domain Join and Validation</h3>
<p>
Joined Client-1 to the domain and verified its presence in Active Directory. Moved the client machine into the <b>_CLIENTS</b> Organizational Unit to maintain structure.
</p>

<p align="center">
  <img src="YOUR_IMAGE_5.png"/>
</p>

---

<h3>Step 6: Remote Desktop Configuration</h3>
<p>
Enabled Remote Desktop access for domain users on Client-1, allowing non-administrative users to log in remotely.
</p>

<p align="center">
  <img src="YOUR_IMAGE_6.png"/>
</p>

---

<h3>Step 7: Bulk User Creation via PowerShell</h3>
<p>
Executed a PowerShell script to generate approximately 10,000 user accounts within Active Directory for testing and simulation purposes. Verified user creation within the _EMPLOYEES Organizational Unit.
</p>

<p align="center">
  <img src="YOUR_IMAGE_7.png"/>
</p>

---

<h3>Step 8: Authentication Testing</h3>
<p>
Tested domain authentication by logging into Client-1 using a newly created user account. Confirmed successful login under domain context.
</p>

---

<h3>Step 9: Account Lockout Policy Configuration</h3>
<p>
Configured Group Policy to enforce account lockout after multiple failed login attempts. Applied the policy and forced an update using <b>gpupdate /force</b>. Verified the policy by triggering account lockouts through repeated failed login attempts.
</p>

---

<h3>Step 10: Account Recovery and Management</h3>
<p>
Unlocked user accounts in Active Directory, reset passwords, and verified successful login after recovery. Tested account disabling and re-enabling to confirm access control behavior.
</p>

<p align="center">
  <img src="YOUR_IMAGE_8.png"/>
</p>

---

<h3>Step 11: Log Analysis</h3>
<p>
Reviewed authentication and security events using Event Viewer on the Domain Controller and client machine to validate login attempts and account activity.
</p>

<p align="center">
  <img src="YOUR_IMAGE_9.png"/>
</p>

---

<h2>✅ Results</h2>

<ul>
  <li>Successfully deployed an Active Directory environment in Azure</li>
  <li>Configured DNS and verified domain communication</li>
  <li>Created and managed users and Organizational Units</li>
  <li>Joined a client machine to the domain</li>
  <li>Implemented and tested account lockout security policies</li>
  <li>Validated authentication and system logs</li>
</ul>

---

<h2>📌 Key Takeaways</h2>

<ul>
  <li>Active Directory is highly dependent on proper DNS configuration</li>
  <li>Static IP configuration is critical for Domain Controllers</li>
  <li>Group Policy provides centralized control over security settings</li>
  <li>PowerShell enables scalable administration of large user environments</li>
  <li>Event logs are essential for monitoring authentication activity</li>
</ul>
