# System Setup & Configuration

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

The goal of this lab is to install and configure an operating system (either Windows or Linux) in this case Windows, on a virtual machine (VM) and document the process. I did some updates in the VM etc.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Azure
- PowerShell


<h2>Operating Systems Used </h2>

- Windows 10 Pro


<h2>High-Level Deployment and Configuration Steps</h2>

- Sign in to Azure Portal
- Create a New Virtual Machine
- Connect to Your Windows VM
- Set Up and Configure Windows
- Run a few Powershell commands 



<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/m5GGkEb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/FGboeUW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/qCFd6lH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/tXayKKc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click + Create → Azure Virtual Machine.

Basics Tab (VM Configuration):

Subscription: Choose your Azure subscription.

Resource Group: Click Create new, name it (e.g., MyRG), and click OK.

Virtual Machine Name: Enter a name (e.g., Win10VM).

Region: Select a nearby region for better performance (e.g., East US).

Availability Options: Leave it as is. No infrastructure redundancy is required.

Image: Select Windows 10 Pro.

Size: Click Change Size and choose a VM size. (e.g., Standard_B2s for testing).

Administrator Account:
Username: Create an admin username (e.g., Labnuser).
Password: Enter and confirm a strong password. (e.g., Password123!)

Inbound Port Rules:
Select Allow RDP (3389) so you can connect via Remote Desktop.

Then Review and create. I had some troubles in Azure with the IP address, that's because I did not clean Azure, remember to erase Resource Groups, etc. Close the app or refresh. 
</p>
<br />


<p>
<img src="https://i.imgur.com/QcLJJbf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/YWvK8od.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
A quick way to connect to the Remote Desktop is to go to connect, select, download that file, and click on it. It saves you the time of copying and pasting the Public IP address. Sign in with your designated username and password. 
</p>
<br />



<p>
<img src="https://i.imgur.com/a4QMIVv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once inside the Windows VM, we're going to install updates and configure some things. As if we are installing this for a user. Some apps were already available

1. Install Updates
Open Settings → Update & Security → Windows Update.
Click Check for updates and install all updates.
Restart the VM if required.
</p>
<p>
<img src="https://i.imgur.com/KBsg9gu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />



<p>
Then we're going to open Powershell as an Administrator (so left-click it).  Then we are going to run some commands. Again a lot of the apps were already installed but still, it's fun to see what I can do, with the different commands. So here are some commands I did. This is what we would do, to make sure a client is all set up. 
</p>
<p>
<img src="https://i.imgur.com/FXApUHC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/FXApUHC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Powershell scripts: (copy and paste) 
  
  Checks network connection: 
  Test-NetConnection -ComputerName google.com -Port 443

  This command installs Google Chrome (which I did just because):  
  winget install --id Google.Chrome -e


  This checks to see if RDP is on. 1 means disabled and 0 means enabled:  
  (Get-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -Name "fDenyTSConnections").fDenyTSConnections

  This command adds the user to the Administrative Group:   
  Add-LocalGroupMember -Group "Administrators" -Member "AdminUser"

  This command creates a new local user:  
  New-LocalUser -Name "AdminUser" -Password (ConvertTo-SecureString "YourPassword123!" -AsPlainText -Force) -FullName "Admin User" -Description "New Admin 
  Account"

  This command checks all running services:   
  Get-Service

  This command creates a new folder and file:  
  New-Item -Path "C:\TestFolder" -ItemType Directory
  New-Item -Path "C:\TestFolder\file.txt" -ItemType File

</p>
<p>
<img src="https://i.imgur.com/w0xAn4b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This is the command we just ran, we have the test folder with the txt.file inside of it
</p>

<br />














