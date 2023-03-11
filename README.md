<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

<p>
In this lab we will create two VMs in the same VNET. One will be a Domain Controller, the other will be a Client machine. We will change the DC to a static IP because its offering Active Directory services to the client machine. Client machine will be joined to the domain. We will control the DNS settings on the client machine, the client machine will use the DC as its DNS server. 
</p>
<br />

<p>
<img src="https://i.imgur.com/z7cqW8Z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Client-1 will need connect to DC-1 to ensure connectivity by pinging DC. So, you should be receiving a request time out message.
</p>
<br />

<p>
<img src="https://i.imgur.com/mEDrATv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To resolve this, we have to enable ICMPv4 on the firewall for DC-1. From there on, we should be receiving replies from DC-1. This is an indication that it is successfully connected.
</p>
<br />

<p>
Next step is to install active directory:
  <ul>
    <li>Login to DC-1 and install Active Directory Domain Services</li>
    <li>Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)</li>
    <li>Restart and then log back into DC-1 as user: mydomain.com\username</li>
  </ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/kcgvzdE.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
From there on we will create an admin and normal user account in active directory
  <ul>
    <li>In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called _EMPLOYEES</li>
    <li>Create a new OU named _ADMINS</li>
    <li>Create a new employee named “Jane Doe” (same password) with the username of jane_admin</li>
    <li>Add jane_admin to the “Domain Admins” Security Group</li>
    <li>Log out/close the Remote Desktop connection to DC-1 and log back in as mydomain.com\jane_admin</li>
    <li>Utilize jane_admin as your admin account from now on</li>
  </ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/jbrGTXW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/Ze0Em5e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Join Client-1 to you your domain
  <ul>
    <li>From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address</li>
    <li>From the Azure Portal, restart Client-1</li>
    <li>Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)</li>
    <li>Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain</li>
  </ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/SApOKiE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Setup Remote Desktop for non-administrative users on Client-1
  <ul>
    <li>Log into Client-1 as mydomain.com\jane_admin and open system properties</li>
      <ul>
        <li>Click Remote Desktop</li>
        <li>Allow domain users access to remote desktop</li>
      </ul>
    <li>You can now log into Client-1 as a normal, non-administrative user now</li>
  </ul>
</p>
<br />

<p>
<img src="https://i.imgur.com/EzWG8ug.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/Gkpe68K.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>
Afer logging into DC-1 as jane_admin, open PowerShell_ise as an administrator to run a script, creating thousands of accounts. 
  <ul>
    <li>When finished, open AUDC and observe the accounts in the appropriate OU</li>
    <li>Log into Client-1 with one of the accounts</li>
  </ul>
</p>
