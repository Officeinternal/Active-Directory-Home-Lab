# Active-Directory-Home-Lab
**Objective: Build a functional Active Directory environment using virtual machines to simulate a real enterprise domain.**

**Lab Architecture**

Hypervisor: Oracle VirtualBox

Domain Controller: Windows Server 2025
- AD DS + DNS
- Static IP
- New forest

Client: Windows 11
- Host‑only networking
- DNS pointed to DC
- Domain‑joined

**Step 1:** Download hypervisor software (Oraclebox for this example):

![Screenshot 1](screenshots/1.png)

**Step 2:** Obtain a Windows Server 2025 ISO and Windows 11 ISO:

![Screenshot 2](screenshots/2.png)
![Screenshot 3](screenshots/3.png)

**Step 3:** Create a VM for Windows Server (Be sure to enable efi and a Host-Only Adapter in network settings):

![Screenshot 4](screenshots/4.png)
![Screenshot 5](screenshots/5.png)

- Setup Admin account and password. (Ex. 3ggm@n123)

**Step 4:** Create the Network for your Domain Controller (Domain Controller promotion was performed through Server Manager, but equivalent PowerShell commands are included for automation)

- Set a static ip address for your Host adapter:

![Screenshot 6](screenshots/6.png)
![Screenshot 7](screenshots/7.png)

- Rename PC to Domain Controller suitable name

- **Powershell commands on Windows Server 2025:**

  **Install Active Directory:** *Install-WindowsFeature AD-Domain-Services -IncludeManagementTools*

  **Promote to Domain Controller:** *Import-Module ADDSDeployment
$pass = Read-Host -AsSecureString "Enter SafeMode password"
Install-ADDSForest -DomainName "[Insert domain name]" -SafeModeAdministratorPassword $pass -InstallDNS -Force*

Or you can create AD and DC through server manager:

- Add Roles and Features:

![Screenshot 8](screenshots/8.png)

- Promote Server to Domain Controller:

![Screenshot 9](screenshots/9.png)
![Screenshot 10](screenshots/10.png)

- Add a new forest since this is a fresh DC:

![Screenshot 11](screenshots/11.png)

**Step 5:** Create OUs, Users and Admins in your AD:

![Screenshot 12](screenshots/12.png)
![Screenshot 13](screenshots/13.png)
![Screenshot 14](screenshots/14.png)
![Screenshot 15](screenshots/15.png)

**Step 6:** Configure a Windows 11 vm client
- Disable network to make a temp local account (otherwise windows will force a Microsoft account login)
- Enable network host-only adapter again

![Screenshot 17](screenshots/17.png)

**Troubleshooting**
*If you run into this issue, make sure to press a key when the text is displayed on the screen or you will receive this pop-up*

![Screenshot 16](screenshots/16.png)

If all is set properly, installation continues:

![Screenshot 18](screenshots/18.png)

Setup the host adapter to share the same dns address as your domain:

![Screenshot 19](screenshots/19.png)

**Step 7:** Join Windows 11 to the Domain
-	System -> About -> Domain -> Reset

![Screenshot 20](screenshots/20.png)
 	
-	Log in as user from domain to test if connected to domain (Ex. Dwight Schrute):

![Screenshot 21](screenshots/21.png)
![Screenshot 22](screenshots/22.png)

**Final step:** Create groups in AD and organize users into them

![Screenshot 23](screenshots/23.png)
![Screenshot 24](screenshots/24.png)
![Screenshot 25](screenshots/25.png)

## Future Labs

Coming soon:
- Group Policy Management
- Permissions & Access Control
- Network Drive Mapping
- Ticketing System Simulation
