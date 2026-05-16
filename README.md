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

- Windows Server 2025 Datacenter X64 Gen2 (x2 for Client VM and Domain Controller VM)

<h2>High-Level Steps</h2>

- Step 1: Configure Account Lockout Security Policies with Group Policy
- Step 2: Simulate Account Lockout and Manage Access in Active Directory
- Step 3: Review Authentication and Security Event Logs

<h2>Deployment and Configuration Steps</h2>

---

## Step 1: Configure Account Lockout Security Policies with Group Policy

---

<p>
<img width="1624" height="981" alt="AD-VM GPM Nav" src="https://github.com/user-attachments/assets/4b2f3e47-eaca-4638-9cbd-a6e6c14cd502" />
</p>
<p>

- Opened Group Policy Management from the domain controller’s Server Manager to begin configuring domain-wide account security policies.

</p>
<br />

<p>
<img width="1624" height="983" alt="AD-VM Default Policy" src="https://github.com/user-attachments/assets/f5fd87c8-16e5-4060-a968-b51970da73e3" />
</p>
<p>

- Navigated to the Default Domain Policy and opened the policy editor to configure account lockout security settings for all domain users.

</p>
<br />

<p>
<img width="1624" height="983" alt="AD-VM Acc Policy NC" src="https://github.com/user-attachments/assets/f723fb50-d46f-4b67-aa4a-c439b77f4b66" />
</p>
<p>

- Navigated to Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy to review the existing domain account lockout settings, which were not yet configured.

</p>
<br />

<p>
<img width="1624" height="983" alt="AD-VM Acc Policy Configured" src="https://github.com/user-attachments/assets/1f147e64-0b77-481d-9d91-6be9c82f66c8" />
</p>
<p>

- Configured domain-wide account lockout settings by setting the threshold to 5 failed login attempts, a 30-minute lockout duration, and enabling administrator account lockout to simulate realistic account security controls.

</p>
<br />

<p>
<img width="1624" height="983" alt="AD-VM Acc Policy Verify" src="https://github.com/user-attachments/assets/96147b40-05a6-4086-9862-1e8ba723bcc3" />
</p>
<p>

- Verified that the account lockout policy settings were successfully applied within the Default Domain Policy, confirming domain-level security enforcement.

</p>
<br />

<p>
<img width="1624" height="983" alt="Client-1 VM gpupdate" src="https://github.com/user-attachments/assets/6cf2202e-92f1-4ba9-8e71-87d27c3db76d" />
</p>
<p>

- Logged into the client virtual machine using administrative credentials and ran gpupdate /force in Command Prompt to immediately apply the updated Group Policy settings.

</p>
<br />

<p>
<img width="1624" height="983" alt="Client-1 VM gpresult" src="https://github.com/user-attachments/assets/ebabc8ac-5a66-45ec-8632-bdf9b2b7e5d0" />
</p>
<p>

- Used gpresult /r to verify that the updated domain Group Policy was successfully applied to the client system.

</p>
<br />

---

## Step 2: Simulate Account Lockout and Manage Access in Active Directory

---

<p>
<img width="662" height="496" alt="Client-1 Failed Login" src="https://github.com/user-attachments/assets/210d0bf5-cab4-4ae6-a6be-639595dcb76a" />
</p>
<p>

- Attempted multiple failed logins on Remote Desktop using a standard domain user account (User: cipaji.dok) to intentionally trigger the configured account lockout policy, confirming the security policy was functioning correctly on the client system.

</p>
<br />

<p>
<img width="1624" height="976" alt="AD-VM Reset PW" src="https://github.com/user-attachments/assets/5b940e91-a09d-4479-b028-bb1d123f5d98" />
</p>
<p>

- Located the locked user account in Active Directory Users and Computers (ADUC), unlocked the account, and reset the password to restore access.

</p>
<br />

<p>
<img width="1624" height="976" alt="AD-VM Account Unlock" src="https://github.com/user-attachments/assets/841359fd-b2d3-4d1b-ac30-94fad7de8694" />
</p>
<p>

- Reviewed additional account management settings within the user’s Active Directory properties, including account unlock status, password controls, and logon restrictions.

</p>
<br />

<p>
<img width="1624" height="979" alt="Client-1 Re-enabled" src="https://github.com/user-attachments/assets/a89d571e-1719-4185-971f-8dac1e012918" />
</p>
<p>

- Logged back into the client system using the previously locked account to confirm successful account recovery and restored domain authentication.

</p>
<br />

<p>
<img width="1624" height="981" alt="AD-VM man-Account Disable" src="https://github.com/user-attachments/assets/4f61629d-12fe-4dd7-aa8d-dda9c84e2001" />
</p>
<p>

- Disabled the user account within Active Directory to simulate access revocation scenarios such as security incidents, offboarding, or role changes.

</p>
<br />

<p>
<img width="662" height="432" alt="Client-1 Acc Disabled" src="https://github.com/user-attachments/assets/cd63ca17-be4e-40bf-a4e9-d64d65b90567" />
</p>
<p>

- Attempted to log into the client system using the disabled account, confirming that authentication was correctly denied due to the account’s disabled status.

</p>
<br />

---

## Step 3: Review Authentication and Security Event Logs

---

<p>
<img width="1624" height="981" alt="Client-1 VM Event Viewer" src="https://github.com/user-attachments/assets/9f1a52bc-a8d9-416b-a31a-e4fafce98608" />
</p>
<p>

- Logged into the client virtual machine using domain administrative credentials and opened Event Viewer to review authentication and security-related system logs.

</p>
<br />

<p>
<img width="1624" height="981" alt="Client-1 VM Security Logs" src="https://github.com/user-attachments/assets/16282ac1-e335-4fc5-80af-4586382ae99e" />
</p>
<p>

- Navigated to Windows Logs → Security and reviewed the failed authentication event generated during the account lockout test, observing details such as the affected user account, client source, and audit failure event information.

</p>
<br />

---

## Skills Developed

### Active Directory User Account Management

Gained hands-on experience managing user accounts within Active Directory Users and Computers (ADUC), including unlocking accounts, resetting passwords, disabling accounts, and restoring user access.

### Group Policy Administration

Configured and applied domain-wide Group Policy security settings, including account lockout thresholds, lockout duration, and authentication policy enforcement.

### Identity and Access Management (IAM) Fundamentals

Developed practical experience with user authentication, access control, account state management, and administrative privilege workflows within a Windows domain environment.

### Account Lockout Troubleshooting

Simulated and resolved common account lockout scenarios by identifying locked accounts, restoring access, and verifying successful user authentication.

### Password Reset and Account Recovery

Performed account recovery procedures including password resets and account unlocks, mirroring common help desk identity support tasks.

### Domain Authentication Management

Tested and verified user authentication behavior for active, locked, and disabled domain accounts within a controlled Active Directory environment.

### Security Policy Enforcement

Configured and validated account security controls designed to reduce unauthorized access attempts and enforce authentication protection across domain-connected systems.

### Event Viewer Log Analysis

Used Event Viewer to review authentication-related security logs, identify failed login attempts, and observe audit event details relevant to user access troubleshooting.

### Windows Client Administration

Managed domain-connected client system settings, applied Group Policy updates, and validated client-side policy enforcement.

### Command Line Administration

Used administrative command-line tools including gpupdate and gpresult to apply and verify Group Policy changes on client systems.

### Security Awareness

Developed awareness of account security practices including failed login protections, access revocation, and authentication auditing.

### Technical Documentation

Documented security policy configuration, account management workflows, and troubleshooting procedures using structured technical documentation and screenshots.
