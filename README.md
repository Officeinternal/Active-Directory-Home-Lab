# Active-Directory-Home-Lab
Objective: To build an Active Directory in a Windows Server 2025 environment using VMs

Step 1: Download hypervisor software (Oraclebox for this example)
![Screenshot 1](screenshots/1.png)
Step 2: Obtain a Windows Server 2025 ISO and Windows 11 ISO

Step 3: Create a VM for Windows Server (Be sure to enable efi and a Host-Only Adaptor in network settings)
-Setup Admin account and password. (Ex. 3ggm@n123)

Step 4: Create the Network for your Domain Controller (Domain Controller promotion was performed through Server Manager, but equivalent PowerShell commands are included for automation)
Set a static ip address for your Host adaptor
Rename PC to Domain Controller suitable name
Powershell commands:
Install Active Directory: Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Promote to Domain Controller: Import-Module ADDSDeployment
$pass = Read-Host -AsSecureString "Enter SafeMode password"
Install-ADDSForest -DomainName "[Insert domain name]" -SafeModeAdministratorPassword $pass -InstallDNS -Force

Or you can create through server manager:
Add Roles and Features
Promote Server to Domain Controller

Step 5: Create OUs, Users and Admins in your AD

Step 6: Configure a Windows 11 vm client
If you run into this issue, make sure to press a key when the text is displayed on the screen or you will receive this pop-up
Enable network host-only adaptor again
Disable network to make a temp local account (otherwise windows will force a microsoft account login)
Setup the host adaptor to share the same dns address as your domain

Step 7: Join your VM to a Domain
-	System -> About -> Domain -> Reset
-	Log in as user from domain to test if connected to domain (Ex. Dwight Schrute)

Final step: Create groups in AD and organize users into them

My next lab will dive into further managing accounts permissions, gp editing, mapping network drives and using a ticketing software. 
