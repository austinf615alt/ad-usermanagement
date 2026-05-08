<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory User Management (Azure)</h1>
This project outlines Active Directory User Management within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Active Directory Users and Computers
- Group Policy Management
- Event Viewer

<h2>Operating Systems Used </h2>

- Windows 11 Pro version 25H2 (For Azure and Remote Desktop)
- Windows Server 2025 Datacenter X64 Gen2 (x2 for Client VM and Domain Controller VM)

<h2>High-Level Steps</h2>

- Step 1: Created and configured Group Policies
- Step 2: Verified Policy Implementation
- Step 3: Performed User Account Management
- Step 4: Investigated Security Events

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="2346" height="1314" alt="LAB5-GROUPPOLICYSETUP" src="https://github.com/user-attachments/assets/62f9c079-fd0f-4160-8c6d-92088a7b0c12" />
</p>
<p>

- Remoted into both Client-1 and Domain-Controller Virtual Machines using Remote Desktop Connection. Used the respective public IP addresses given to both Virtual Machines to sign in and used a domain administrator account to log in.

- After signing in to the domain controller, opened Server Manager and navigated to Group Policy Management. Within the domain structure, edited the Default Domain Policy to configure an account lockout policy, defining account lockout thresholds, and account lockout durations. These changes were applied at the domain level to enforce consistent security controls across all user accounts.

</p>
<br />

<p>
<img width="2346" height="1314" alt="LAB5-GROUPPOLICYVERIFY" src="https://github.com/user-attachments/assets/66301d5f-8919-4b31-ae3a-567d6da8b42a" />
</p>
<p>
  
- After configuring the account lockout policy, returned to Group Policy Management to verify that the Default Domain Policy had been successfully updated and applied at the domain level. Confirmed proper configuration of lockout thresholds and validated policy propagation to ensure enforcement across all domain-joined systems.

- After updating the Default Domain Policy, remoted into Client-1 Virtual Machine under the domain administrator account, and opened Powershell to run "gpupdate /force" to refresh and apply the updated Group Policy settings on the client machine. Policy application was then verified to ensure the account lockout configuration was correctly enforced across the domain.

</p>
<br />

<p>
<img width="2346" height="1314" alt="LAB5-LOCKOUT" src="https://github.com/user-attachments/assets/5de19b29-7b74-4de4-be9b-fad4405c988d" />
</p>
<p>

- On the Domain-Controller Virtual Machine, added a non-administrator user under the _EMPLOYEES organizational unit in Active Directory. Signed out of the domain administrator account on the Client-1 Virtual Machine and attempted to sign in with nonadmin user "bab.feli", intentionally entering the wrong password 5 times, meeting the account lockout threshold. Note that the account is locked out as expected. The account may be managed through Active Directory Users and Computers, passwords may also be reset here as well as log on hour restrictions and workstation restrictions.

<br />

<p>
<img width="1792" height="1072" alt="LAB5-SECURITYLOGS" src="https://github.com/user-attachments/assets/4b5c905b-0e8f-4099-9235-f16955781b35" />
</p>
<p>

- After confirming the account lockout in Active Directory, opened Event Viewer on the Client-1 virtual machine and reviewed the Security logs. Located an Account Lockout event under the task category, verifying that the lockout was triggered by multiple failed authentication attempts on the Client-1 system in accordance with the configured Group Policy. 

</p>
<br />
