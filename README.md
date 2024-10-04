<p align="center">
  <img src="https://github.com/user-attachments/assets/a9e62984-6877-41d3-b24c-25d0460b9005" alt="Microsoft Azure logo">
</p>

<h1>Configuring Active Directory within Azure VMs</h1>

<p>This tutorial outlines the configuration of Active Directory within Azure Virtual Machines. You'll learn how to set up a domain controller, join a client machine to the domain, and configure user roles and permissions in a lab environment.</p>

<h2>Part 1: Setup Domain Controller and Client in Azure</h2>

<p><strong>Step 1: Create a Resource Group and Virtual Network</strong></p>
<ul>
  <li>In the Azure Portal, create a new resource group for the lab environment.</li>
  <li>Create a virtual network with a subnet to host both the Domain Controller (DC) and Client machine.</li>
</ul>

<p><strong>Step 2: Create Domain Controller (DC-1)</strong></p>
<ul>
  <li>In the Azure Portal, create a Windows Server 2022 VM named <strong>DC-1</strong>.</li>
  <li>Use the following credentials: Username: <strong>labuser</strong>, Password: <strong>Cyberlab123!</strong></li>
  <li>Set DC-1's NIC private IP address to static in the Azure Portal.</li>
  <li>Log in to the VM and disable the Windows Firewall (for testing purposes).</li>
</ul>

<p><strong>Step 3: Create Client VM (Client-1)</strong></p>
<ul>
  <li>Create a Windows 10 VM named <strong>Client-1</strong> and attach it to the same virtual network as DC-1.</li>
  <li>Use the following credentials: Username: <strong>labuser</strong>, Password: <strong>Cyberlab123!</strong></li>
  <li>Set Client-1's DNS settings to DC-1's private IP address.</li>
  <li>Restart Client-1 from the Azure Portal.</li>
  <li>Log in to Client-1 and ping DC-1’s private IP address to ensure connectivity.</li>
</ul>

<p><strong>Step 4: Install Active Directory on DC-1</strong></p>
<ul>
  <li>Log in to DC-1 and install Active Directory Domain Services (AD DS).</li>
  <li>Promote DC-1 to a Domain Controller and set up a new forest as <strong>mydomain.com</strong>.</li>
  <li>Restart DC-1 and log in as <strong>mydomain.com\labuser</strong>.</li>
</ul>

<p><strong>Step 5: Create Domain Admin User</strong></p>
<ul>
  <li>In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called <strong>_ADMINS</strong>.</li>
  <li>Create a new user named <strong>jane_admin</strong> with the password <strong>Cyberlab123!</strong>.</li>
  <li>Add <strong>jane_admin</strong> to the <strong>Domain Admins</strong> security group.</li>
  <li>Log out and log back in as <strong>mydomain.com\jane_admin</strong>.</li>
</ul>

<h2>Part 2: Join Client-1 to the Domain</h2>

<p><strong>Step 6: Configure Client-1</strong></p>
<ul>
  <li>Set Client-1’s DNS settings to DC-1’s private IP address (already done in Step 3).</li>
  <li>Restart Client-1 from the Azure Portal (already done in Step 3).</li>
  <li>Log in to Client-1 as <strong>labuser</strong> and join it to the domain <strong>mydomain.com</strong>.</li>
  <li>Restart Client-1 and log in to verify that Client-1 is now part of the domain.</li>
  <li>Create an OU named <strong>_CLIENTS</strong> and move Client-1 into it within ADUC.</li>
</ul>

<h2>Part 3: Setup Remote Desktop and Create Additional Users</h2>

<p><strong>Step 7: Setup Remote Desktop for Non-Admin Users</strong></p>
<ul>
  <li>Log in to Client-1 as <strong>mydomain.com\jane_admin</strong>.</li>
  <li>Open System Properties, click on <strong>Remote Desktop</strong>, and allow <strong>domain users</strong> access to Remote Desktop.</li>
  <li>Verify that normal, non-administrative users can log into Client-1 remotely.</li>
</ul>

<p><strong>Step 8: Create Additional Users in Active Directory</strong></p>
<ul>
  <li>Log in to DC-1 as <strong>jane_admin</strong>.</li>
  <li>Open PowerShell ISE as an administrator and run a script to create multiple user accounts.</li>
  <li>Observe the accounts being created in the <strong>_EMPLOYEES</strong> OU within ADUC.</li>
  <li>Attempt to log into Client-1 with one of the newly created user accounts.</li>
</ul>

<h2>Part 4: Dealing with Account Lockouts and Monitoring Logs</h2>

<p><strong>Step 9: Configure Account Lockout Policy</strong></p>
<ul>
  <li>Log in to DC-1 and configure Group Policy to lock out accounts after 5 failed login attempts.</li>
  <li>Attempt to log in with a user account multiple times to trigger the lockout.</li>
  <li>Observe the account being locked out in Active Directory and unlock it.</li>
</ul>

<p><strong>Step 10: Monitor Logs</strong></p>
<ul>
  <li>Observe the logs on DC-1 and Client-1 to monitor login attempts and other activities.</li>
  <li>Discuss the importance of logging and monitoring in security operations.</li>
</ul>

<h2>Conclusion</h2>
<p>Congratulations! You have successfully set up Active Directory within Azure Virtual Machines. You've learned how to configure a Domain Controller, join a client machine to the domain, manage user accounts, and configure Remote Desktop access. These configurations are crucial in real-world IT environments where Active Directory plays a key role in user management and security.</p>
