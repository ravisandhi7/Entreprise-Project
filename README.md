📌 **Overview**

This project demonstrates a complete Enterprise Active Directory environment built using virtual machines. It simulates a real-world corporate network with multiple domain controllers, organizational units, and group policies.

The lab is designed to showcase system administration, identity management, and enterprise network configuration skills.

🎯 **Objectives**


Deploy and configure Active Directory Domain Services (AD DS)


Implement multi-domain controller architecture


Configure DNS and DHCP services


Create and manage Organizational Units (OUs), Users, and Groups


Apply Group Policies (GPOs)


Test replication and domain functionality


🖥️ **Lab Environment**


Virtual Machines


Machine	Role	IP Address


ROOTDC - Server1 - Primary Domain Controller	10.0.0.1/8


ADC - Server100 - Additional Domain Controller	10.0.0.100/8


RODC - Server101 - Read-Only Domain Controller	10.0.0.101/8


Client PC - PC1 - 10.0.0.160/8



![IPCONFIG](screenshots/basic/IPCONFIG_ALL.png)


![IPCONFIG](screenshots/basic/IPCONFIG_ALL_DHCP_DNS.png)


![PING](screenshots/basic/PING_ROOTDC_ADC.png)


![PING](screenshots/basic/PING_RODC.png)


PC1	Windows 11	DHCP(Reserved IP)


Network Configuration


NAT Network


DNS handled by ROOTDC


DHCP configured on ROOTDC


🏗️ **Architecture**


ROOTDC → AD DS, DNS, DHCP


ADC → Additional Domain Controller (Replication)


RODC → Read-Only Domain Controller


Client Machine → Domain-joined workstation


![PING RODC](screenshots/basic/COMPUTERS_IN_DOMAIN.png)


![PING RODC](screenshots/basic/DOMAIN_CONTROLLERS_ROOTDC_ADC_RODC.png)


🧑‍💼 **Active Directory Structure**


Domain: ravikumar.online


OUs: HR, IT, Finance


Groups: HR_GROUP, FINANCE_GROUP, IT_GROUP


👥 **Users and Groups**


Sample Users


HR: hruser1, hruser2

![PING RODC](screenshots/users/HR_USERS.png)


IT: ituser1, ituser2

![PING RODC](screenshots/users/IT_USERS.png)


Finance: financeuser1, financeuser2


![PING RODC](screenshots/users/FINANCE_USERS.png)


RODC: rodcuser1, rodcuser2


![RODC USERS](screenshots/users/RODC_USERS.png)


Security Groups


HR_Group


IT_Group


Finance_Group


![PING RODC](screenshots/groups/GROUPS.png)



🌐**Services Configured**


✅ **Active Directory Domain Services**


Forest: ravikumar.online


✅ **DNS**


Integrated with AD


✅**DHCP**


Scope: 10.0.0.150 – 10.0.0.165


Gateway: 10.0.0.1


DNS: 10.0.0.1


![DHCP](screenshots/basic/DHCP_ADDRESS_POOL.png)


![DHCP](screenshots/basic/DHCP_ADDRESS_LEASE.png)



🔁**Domain Controllers**


ADC (Additional Domain Controller)


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


![GPO](screenshots/gpo/GP_HR_USB_DESKTOP_RESTRICTION.png)


![GPO](screenshots/gpo/HR_USB_BLOCK.png)


![GPO](screenshots/gpo/HR_USB_BLOCK_TO_HR_OU.png)


![GPO](screenshots/gpo/DEFAULT_DOMAIN_PASSWORD.png)


![GPO](screenshots/gpo/DEFAULT_DOMAIN_PASSWORD_TO_DC_OU.png)


![GPO](screenshots/gpo/HR_DESKTOP_RESTRICTIONS.png)


![GPO](screenshots/gpo/HR_DESKTOP_RESTRICTIONS_TO_HR_OU.png)


![GPO](screenshots/gpo/GPUPDATE_FORCE.png)


🧪 **Testing & Validation**


✔ Domain user login on client


✔ DHCP IP assignment


✔ GPO application verification


✔ AD replication check


Commands used:


repadmin /showrepl


gpupdate /force


📸**Screenshots**


Stored in: screenshots/


Includes:


AD structure


Users and groups


DHCP configuration


GPO settings


Client login

    
🚀 **Key Skills Demonstrated**

Active Directory Administration


Windows Server Management


DNS & DHCP Configuration


Group Policy Management


Enterprise Network Design


Troubleshooting & Replication


🧠 **Learning Outcomes**


This lab provides hands-on experience in building and managing a realistic enterprise IT infrastructure, preparing for roles such as:


System Administrator


IT Support Specialist


Network Administrator
