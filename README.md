<p align="center">
  <img src="https://github.com/user-attachments/assets/a9e62984-6877-41d3-b24c-25d0460b9005" alt="Microsoft Azure logo">
</p>

<h1>Configuring Active Directory within Azure VMs</h1>

<p>In this lab, I will walk you through how I set up Active Directory within Azure Virtual Machines. I’ll configure a domain controller, join a client machine to the domain, and manage user roles and permissions in a simulated IT environment.</p>

<h2>Part 1: Setting Up the Domain Controller and Client in Azure</h2>

<p><strong>Step 1: Create a Resource Group and Virtual Network</strong></p>
<ul>
  <li>First, I created a new resource group in the Azure Portal to organize my resources for the lab.</li>
  <li>Then, I set up a virtual network with a subnet that will host both the Domain Controller (DC-1) and the client machine (Client-1).</li>
</ul>




<p align="center">
  <img src="https://github.com/user-attachments/assets/febb8a2c-43d1-4235-bb2b-633326f0edac" alt="Creating Resource Group and Virtual Network" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/c63019b8-7327-4327-aee3-ee54e0b5de1d" alt="Creating Resource Group and Virtual Network" width="80%">
</p>


<p><strong>Step 2: Create Domain Controller (DC-1)</strong></p>
<ul>
  <li>Next, I created a Windows Server 2022 VM named <strong>DC-1</strong> in the Azure Portal.</li>
  <li>I used the following credentials: Username: <strong>labuser</strong>, Password: <strong>Cyberlab123!</strong>.</li>
  <li>I set DC-1's NIC private IP address to static in the Azure Portal to ensure consistency.</li>
  <li>Once I logged into the VM, I disabled the Windows Firewall temporarily for testing connectivity purposes.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/db00c4e8-d807-41a5-a342-d684ac2cb4d4" alt="Creating Domain Controller" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/a287d57a-f675-4700-9e0b-d5e1935a2e50" alt="Creating Resource Group and Virtual Network" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/2fda670c-aa47-447d-8602-e681169db750" alt="Creating Resource Group and Virtual Network" width="80%">
</p>



<p><strong>Step 3: Create Client VM (Client-1)</strong></p>
<ul>
  <li>Similarly, I created a Windows 10 VM named <strong>Client-1</strong> and attached it to the same virtual network as DC-1.</li>
  <li>I used the same credentials as DC-1: Username: <strong>labuser</strong>, Password: <strong>Cyberlab123!</strong>.</li>
  <li>Then, I set Client-1’s DNS settings to point to DC-1’s private IP address.</li>
  <li>After restarting Client-1 from the Azure Portal, I logged in and pinged DC-1’s private IP address to confirm connectivity.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/025152d9-0bfa-4cdc-b2b0-ac72b1ba9818" alt="Creating Client VM" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/be01001e-02f2-427f-b61e-2ff2a4afa27d" alt="Creating Client VM" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/78fb615b-99c0-4f72-9a55-ed4710ab1d77" alt="Creating Client VM" width="80%">
</p>



<h2>Part 2: Installing and Configuring Active Directory</h2>

<p><strong>Step 4: Install Active Directory on DC-1</strong></p>
<ul>
  <li>I logged back into DC-1 and installed Active Directory Domain Services (AD DS).</li>
  <li>Afterward, I promoted DC-1 to a Domain Controller and set up a new forest with the domain name <strong>mydomain.com</strong>.</li>
  <li>I restarted DC-1 and logged back in using <strong>mydomain.com\labuser</strong> to continue configuration.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/7ed8a091-27cf-4e91-b962-071252f13986" alt="Installing AD DS on DC-1" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/4016ca2f-712a-4a2d-9db4-933a6606aeb3" alt="Installing AD DS on DC-1" width="80%">
</p>



<p><strong>Step 5: Create a Domain Admin User</strong></p>
<ul>
  <li>Using Active Directory Users and Computers (ADUC), I created an Organizational Unit (OU) called <strong>_ADMINS</strong>.</li>
  <li>I created a new user named <strong>pablo_davis</strong> with the password <strong>Cyberlab123!</strong>, and added her to the <strong>Domain Admins</strong> security group.</li>
  <li>Finally, I logged out and logged back in as <strong>mydomain.com\pablo_davis</strong>, which I will use as my admin account going forward.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/6a413707-bd21-4419-a008-e3c3db826127" alt="Creating Domain Admin User" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/175e1dd8-8f4a-4a77-8270-7b7fb4114e4f" alt="Creating Domain Admin User" width="80%">
</p>


<h2>Part 3: Joining Client-1 to the Domain</h2>

<p><strong>Step 6: Configure Client-1 and Join the Domain</strong></p>
<ul>
  <li>With Client-1’s DNS settings pointing to DC-1’s private IP address, I restarted the VM and logged in as <strong>labuser</strong>.</li>
  <li>I joined Client-1 to the domain <strong>mydomain.com</strong>, restarted the machine, and verified the successful domain join by logging in.</li>
  <li>Within ADUC, I created a new OU named <strong>_CLIENTS</strong> and moved Client-1 into it for proper organization.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/f0b5e7c2-3ab3-4319-8aba-6a8fd1041587" alt="Joining Client-1 to Domain" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/f7d68ad7-20f9-40a1-9ece-164e67987ba5"alt="Joining Client-1 to Domain" width="80%">
</p>

<h2>Part 4: Setting Up Remote Desktop and Creating Additional Users</h2>

<p><strong>Step 7: Enable Remote Desktop for Non-Admin Users</strong></p>
<ul>
  <li>Logging into Client-1 as <strong>mydomain.com\pablo_davis</strong>, I enabled Remote Desktop access for domain users under System Properties.</li>
  <li>This allows non-administrative users to remotely access Client-1.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/37931436-df88-447d-8512-60622493508b" alt="Setting Up Remote Desktop" width="80%">
</p>





<p><strong>Step 8: Create Additional Users in Active Directory</strong></p>
<ul>
  <li>Returning to DC-1, I logged in as <strong>pablo_davis</strong> and opened PowerShell ISE as an administrator to run a script that created multiple user accounts.</li>
  <li>Once the accounts were created, I observed them in the <strong>_EMPLOYEES</strong> OU within ADUC.</li>
  <li>I tested one of the newly created accounts (bam.wed) by logging into Client-1.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/202d39d3-d14a-4aeb-ae21-29d22060a340" alt="Creating Additional Users" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/96775b63-876f-43e6-99aa-6cf24a6ca4a5" alt="Creating Additional Users" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/697d6d87-cdcd-43ef-9b43-ae8c9bddca53" alt="Creating Additional Users" width="80%">
</p>




<h2>Part 5: Managing Account Lockouts and Monitoring Logs</h2>

<p><strong>Step 9: Configure Account Lockout Policy</strong></p>
<ul>
  <li>Back on DC-1, I configured Group Policy to lock accounts after 5 failed login attempts.</li>
  <li>I tested this by attempting to log in with an incorrect password multiple times, triggering the lockout, and then unlocked the account in Active Directory.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/eab6289c-af3a-4bf3-870f-dcf03e10e8df" alt="Configuring Account Lockout Policy" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/fdc22ce5-051a-44ca-a2f3-e2f3126f2ade" alt="Configuring Account Lockout Policy" width="80%">

</p><p align="center">
  <img src="https://github.com/user-attachments/assets/f17ae2c7-5178-4989-8250-6c77761242b9" alt="Configuring Account Lockout Policy" width="80%">
</p>

</p><p align="center">
  <img src="https://github.com/user-attachments/assets/52b2b089-c4ac-4223-9425-c54d36eb6d81" alt="Configuring Account Lockout Policy" width="80%">
</p>



<p><strong>Step 10: Monitor Logs</strong></p>
<ul>
  <li>To wrap things up, I observed the logs on both DC-1 and Client-1 to monitor login attempts and other activities.</li>
  <li>This demonstrated the importance of logging and monitoring in security operations, a critical skill for network management.</li>
</ul>
<p align="center">
  <img src="IMAGE_URL_HERE" alt="Monitoring Logs" width="80%">
</p>

<h2>Conclusion</h2>
<p>I successfully set up Active Directory within Azure Virtual Machines. This lab allowed me to practice configuring a Domain Controller, joining a client machine to the domain, managing user accounts, and enabling Remote Desktop access. These configurations are essential in real-world IT environments for ensuring secure and efficient user management.</p>
