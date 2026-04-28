📌 **Overview**

This project demonstrates a complete Enterprise Active Directory environment built using virtual machines. It simulates a real-world corporate network with multiple domain controllers, organizational units, group policies, and automation using PowerShell.

The lab is designed to showcase system administration, identity management, and enterprise network configuration skills.

🎯 **Objectives**


Deploy and configure Active Directory Domain Services (AD DS)


Implement multi-domain controller architecture


Configure DNS and DHCP services


Create and manage Organizational Units (OUs), Users, and Groups


Automate user creation using PowerShell


Apply Group Policies (GPOs)


Test replication and domain functionality


🖥️ **Lab Environment**


Virtual Machines


Machine	Role	IP Address


DC1	Primary Domain Controller	10.0.0.10


DC2	Additional Domain Controller	10.0.0.11


RODC	Read-Only Domain Controller	10.0.0.12

![PING RODC](screenshots/basic/PING_RODC.png)


Client	Windows 10/11	DHCP


Network Configuration


Internal Network / Host-Only Adapter


DNS handled by DC1


DHCP configured on DC1


🏗️ **Architecture**


DC1 → AD DS, DNS, DHCP


DC2 → Additional Domain Controller (Replication)


RODC → Read-Only Domain Controller


Client Machine → Domain-joined workstation


![PING RODC](screenshots/basic/COMPUTERS_IN_DOMAIN.png)


![PING RODC](screenshots/basic/DOMAIN_CONTROLLERS_ROOTDC_ADC_RODC.png)


📌 **See: architecture-diagram.png**


⚙️ **Setup Guide**


Detailed step-by-step instructions are available in:


📄 **setup-guide.md**

🧑‍💼 **Active Directory Structure**


Enterprise.local

HR


IT



Finance


Groups


👥 **Users and Groups**


Sample Users


HR: hr.user1, hr.user2


IT: it.user1, it.admin


Finance: finance.user1


Security Groups


HR_Group


IT_Group


Finance_Group


⚡**PowerShell Automation**

User creation automated using:

📄**scripts/create-users.ps1**

Features:


Bulk user creation


OU-based organization


Secure password setup


Enabled accounts by default


🌐**Services Configured**


✅ **Active Directory Domain Services**


New forest: enterprise.local


✅ **DNS**


Integrated with AD


Optional forwarder: 8.8.8.8


✅**DHCP**


Scope: 10.0.0.100 – 10.0.0.200


Gateway: 10.0.0.1


DNS: 10.0.0.10


🔁**Domain Controllers**


DC2 (Additional Domain Controller)


Joined to domain


Replication verified using:


repadmin /replsummary


RODC (Read-Only Domain Controller)


Configured with selective password caching:


❌ **HR & Finance → Denied**


✅ **IT → Allowed**


🔐**Group Policy (GPO)**

Implemented policies include:

USB storage restriction (HR)


Password policies


Desktop restrictions


Managed via:


Group Policy Management Console (GPMC)


🧪 **Testing & Validation**


✔ Domain user login on client


✔ DHCP IP assignment


✔ GPO application verification


✔ AD replication check


Commands used:


repadmin /showrepl


📸**Screenshots**


Stored in: screenshots/


Includes:


AD structure


Users and groups


DHCP configuration


GPO settings


Replication status


Client login


📂 **Repository Structure**


Enterprise-Active-Directory-Lab/
│
├── README.md
├── architecture-diagram.png
├── setup-guide.md
├── scripts/
│   └── create-users.ps1
├── screenshots/
│   ├── ad-structure.png
│   ├── dhcp-scope.png
│   ├── gpo.png
│   └── replication.png
└── notes/
    └── troubleshooting.md

    
🚀 **Key Skills Demonstrated**

Active Directory Administration


Windows Server Management


PowerShell Automation


DNS & DHCP Configuration


Group Policy Management


Enterprise Network Design


Troubleshooting & Replication


🧠 **Learning Outcomes**


This lab provides hands-on experience in building and managing a realistic enterprise IT infrastructure, preparing for roles such as:


System Administrator


IT Support Specialist


Network Administrator
