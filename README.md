1. Prerequisites 
You need 3–4 VMs in VirtualBox / VMware:
•	DC1 (Primary Domain Controller) → Windows Server 2019/2022 
•	DC2 (Additional Domain Controller) 
•	RODC Server 
•	(Optional) Client Windows 10/11 machine 
Network Setup
Use Internal Network or Host-Only Adapter
Example IP plan:
Machine	IP Address
DC1	10.0.0.10
DC2	10.0.0.11
RODC	10.0.0.12
Client	DHCP


![PING RODC](screenshots/basic/PING_RODC.png)


2. Build Primary Domain Controller (DC1)
Step 1: Install AD DS Role
•	Server Manager → Add Roles 
•	Select: 
o	Active Directory Domain Services 
o	DNS Server 
Step 2: Promote to Domain Controller
•	Choose: 
o	“Add new forest” 
o	Domain: enterprise.local 
Restart server.

Step 3: Configure DNS
•	Ensure DNS role installed 
•	Set forwarders (optional): 8.8.8.8 
________________________________________
3. Create OU Structure (Very Important for Resume)
Open:
Active Directory Users and Computers (ADUC)
Create:
Enterprise.local
│
├── HR
├── IT
├── Finance
└── Groups

4. Create Users + Groups
Manual method (for screenshots):
Create:
•	HR Users: hr.user1, hr.user2 
•	IT Users: it.user1, it.admin 
•	Finance Users: finance.user1 
Create Security Groups:
•	HR_Group 
•	IT_Group 
•	Finance_Group 
Assign users → groups.

5. PowerShell Automation (IMPORTANT FOR GITHUB)
Create file: create-users.ps1
Import-Module ActiveDirectory

$users = @(
    @{Name="HR User1"; OU="HR"},
    @{Name="IT User1"; OU="IT"},
    @{Name="Finance User1"; OU="Finance"}
)

foreach ($user in $users) {
    $username = $user.Name.Replace(" ","").ToLower()

    New-ADUser `
        -Name $user.Name `
        -SamAccountName $username `
        -UserPrincipalName "$username@enterprise.local" `
        -Path "OU=$($user.OU),DC=enterprise,DC=local" `
        -AccountPassword (ConvertTo-SecureString "Password@123" -AsPlainText -Force) `
        -Enabled $true
}

6. Add Second Domain Controller (DC2 - ADC)
On DC2:
Step 1:
•	Join domain: enterprise.local 
Step 2:
•	Install AD DS role 
Step 3:
•	Promote → “Add domain controller to existing domain” 
Verify replication:
repadmin /replsummary

7. Setup RODC (Read Only Domain Controller)
On RODC server:
•	Join domain 
•	Promote: 
o	Select “Read Only Domain Controller” 
Important settings:
•	Deny password caching for HR/Finance groups 
•	Allow IT group caching 

![DC_ROOTDC_ADC_RODC](screenshots/basic/DOMAIN_CONTROLLERS_ROOTDC_ADC_RODC.png)


8. DHCP Setup
On DC1:
•	Install DHCP role 
•	Create scope: 
Example:
Range: 10.0.0.100 - 10.0.0.200
Gateway: 10.0.0.1
DNS: 10.0.0.10
Authorize DHCP in AD.

![DHCP_ADDRESS_POOL](screenshots/basic/DHCP_ADDRESS_POOL.png)



9. Group Policy (VERY IMPORTANT FOR RESUME)
Create GPOs:
Example Policies:
•	Disable USB (HR computers) 
•	Password policy 
•	Desktop restrictions 
Path:
Group Policy Management → Default Domain Policy / New GPO

10. Testing (You MUST show this in screenshots)
•	Login with domain user on client machine 
•	Check: 
o	IP from DHCP 
o	User login works 
o	Group policies applied 
•	Test replication: 
repadmin /showrepl

11. Screenshots You MUST Include on GitHub
Take screenshots of:
•	AD Users & Computers (OU structure) 
•	Created users 
•	Group membership 
•	DHCP scope 
•	GPO settings 
•	DC1 + DC2 replication status 
•	Client login screen 

12. Architecture Diagram (draw.io)
Include:
•	DC1 (AD DS + DNS + DHCP) 
•	DC2 (ADC) 
•	RODC 
•	Client machines 
•	Network switch (virtual) 
Export as:
architecture-diagram.png

13. GitHub Repository Structure
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
