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
Client-1 will need connect to DC-1 to ensure connectivity by pinging DC. So, you be receiving a request time out message.
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
    <li>Promote as a DC: Setup a new forest as mydomain.com (can be anything, just         remember what it is)</li>
    <li>Restart and then log back into DC-1 as user: mydomain.com\username</li>
  </ul>
</p>
<br />

<p>
Next step is to install active directory:
  <ul>
    <li></li>
    <li></li>
    <li></li>
  </ul>
</p>
<br />

