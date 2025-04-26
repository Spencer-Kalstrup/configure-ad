<p align="center"><img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/></p>

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

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Domain Controller and Client in Azure
- Install Active Directory
- Step 3
- Step 4



<h2>Creating and Configuring a Domain Controller in Azure</h2>
To create a domain controller, open Azure and click "Resource Groups".
<p><img src="https://i.imgur.com/IaDRU8l.png" height="80%" width="80%"/></p>
<br />
Click "Create".
<p><img src="https://i.imgur.com/AywQdZt.png" height="80%" width="80%"/></p>
<br />
Name the resource group "Active-Directory-Lab" and set the region to Canada Central. The region needs to be the same for the client virtual machine. Click create.
<p><img src="https://i.imgur.com/hLst4wt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/></p>
<br />
Click "Virtual Machines".
<p><img src="https://i.imgur.com/88g7Zuv.png" height="80%" width="80%"/></p>
<br />
Click "Azure Virtual Machine".
<p><img src="https://i.imgur.com/O6n2XXa.png" height="80%" width="80%"/></p>
<br />
Make sure the resource group is set to Active-Directory-Lab. Name the Virtual machine Active-Directory-Server. Set the region to Canada Central.
<p><img src="https://i.imgur.com/AGN3V9m.png" height="80%" width="80%"/></p>
<br />
Scroll down and under "Image" select "Windows Server 2022 Datacenter: Azure Edition - x64 Gen2".
<p><img src="https://i.imgur.com/mADtZCu.png" height="80%" width="80%"/></p>
<br />
Under "Size" select at least 2 vcpus and 8 GB of RAM.
<p><img src="https://i.imgur.com/LPMzACT.png" height="80%" width="80%"/></p>
<br />
Username and Password here will be the credentials used in remote desktop. For this lab I used the username: labuser, and password: Cyberlab123! Click "Next".
<p><img src="https://i.imgur.com/oseBjpz.png" height="80%" width="80%"/></p>
<br />
Click "Networking".
<p><img src="https://i.imgur.com/6IXVULY.png" height="80%" width="80%"/></p>
<br />
Under "Virtual Network", make sure "Active-Directory-Server-vnet" is selected. Click "Review + Create"
<p><img src="https://i.imgur.com/d6SGSYn.png" height="80%" width="80%"/></p>
<br />
Once the Virtual Machine is deployed, click "Go to resource".
<p><img src="https://i.imgur.com/U6zPwy8.png" height="80%" width="80%"/></p>
<br />
Click "Network settings"
<p><img src="https://i.imgur.com/pSzL3uS.png" height="80%" width="80%"/></p>
<br />
Click "active-directory-server417_z1 (primary) / ipconfig1 (primary)".
<p><img src="https://i.imgur.com/c2MOLO6.png" height="80%" width="80%"/></p>
<br />
Click "ipconfig1"
<p><img src="https://i.imgur.com/80XE6fH.png" height="80%" width="80%"/></p>
<br />
Click the circle next to "Static"
<p><img src="https://i.imgur.com/obiVNNe.png" height="80%" width="80%"/></p>
<br />
This box should auto-fill. Remember this number labeled "Active Directory Server Private IP Address. In this case, it will be "10.0.0.4". Clic "Save".
<p><img src="https://i.imgur.com/3jFRDDy.png" height="80%" width="80%"/></p>
<br />
Navigate back to the "Home" page.
<p><img src="https://i.imgur.com/O2e8kHB.png" height="80%" width="80%"/></p>
<br />
Click "Active-directory-server"
<p><img src="https://i.imgur.com/d1bHDFl.png" height="80%" width="80%"/></p>
<br />
Copy the public IP address
<p><img src="https://i.imgur.com/bYwjKAR.png" height="80%" width="80%"/></p>
<br />
Open Remote Desktop. Click the + symbol to add a new PC.
Enter the public IP address where it says "PC Name". Click "Add".
<p><img src="https://i.imgur.com/i9JSNRd.png" height="80%" width="80%"/></p>
<br />
Once logged into the Domain Controller, right-click the windows icon in the bottom-left corner and click "run". 
<p><img src="https://i.imgur.com/aCzMfCF.png" height="80%" width="80%"/></p>
<br />
Type "wf.msc". This will open windows firewall.
<p><img src="https://i.imgur.com/3yFuGgH.png" height="80%" width="80%"/></p>
<br />
Click "Windows Defender Firewall Properties"
<p><img src="https://i.imgur.com/A2At6Oz.png" height="80%" width="80%"/></p>
<br />
Under the "Domain Profile" tab, set Firewall state to "Off".
<p><img src="https://i.imgur.com/BOpgFe9.png" height="80%" width="80%"/></p>
<br />
Navigate to the "Private Profile" tab, set the Firewall state to "Off".
<p><img src="https://i.imgur.com/Nz8hkZs.png" height="80%" width="80%"/></p>
<br />
Navigate to the "Public Profile" tab, set the Firewall state to "Off".
<p><img src="https://i.imgur.com/vW5Jnai.png" height="80%" width="80%"/></p>
<br />
Click "Apply".
<p><img src="https://i.imgur.com/PsQno18.png" height="80%" width="80%"/></p>
<br />
The Domain Controller is now setup and ready to test!

<h2>Creating and Configuring a Client in Azure</h2>
Navigate to "Virtual Machines".
<p><img src="https://i.imgur.com/Z1LE57L.png" height="80%" width="80%"/></p>
<br />
Click "Azure Virtual Machine".
<p><img src="https://i.imgur.com/bqGIYy6.png" height="80%" width="80%"/></p>
<br />
Assign the resource group "Active-Directory-Lab". Name the Virtual Machine "Client-1". Set the region to Canada Central, the same as the Domain Controller.
<p><img src="https://i.imgur.com/pTFdorc.png" height="80%" width="80%"/></p>
<br />
Set "Image to "Windows 10 Pro". Set the "Size" to at least 2 vcpus, and 8 GB of memory.
<p><img src="https://i.imgur.com/dQ8raI3.png" height="80%" width="80%"/></p>
<br />
Set username: "labuser", and password: "Cyberlab123!", these will be the credentials used to log in from Remote Desktop. Click "Next: Disks".
<p><img src="https://i.imgur.com/MjaI5Dw.png" height="80%" width="80%"/></p>
<br />
Click "Next: Networking".
<p><img src="https://i.imgur.com/XJPapri.png" height="80%" width="80%"/></p>
<br />
Set the "Virtual Network" to "Active-Directory-Server-vnet". Click "manage subnet configuration".
<p><img src="https://i.imgur.com/EifuKJf.png" height="80%" width="80%"/></p>
<br />
Click "DNS servers".
<p><img src="https://i.imgur.com/lGxuIZs.png" height="80%" width="80%"/></p>
<br />
Click the circle next to "Custom". Enter the private IP address of the Domain Controller we saved from earlier. In this case, it is "10.0.0.4". Click "Save". Click "Create a virtual machine".
<p><img src="https://i.imgur.com/kx17Uvj.png" height="80%" width="80%"/></p>
<br />
Click "Review + Create". Once the Virtual Machine is deployed, click "Go to resource".
<p><img src="https://i.imgur.com/M4zzhLY.png" height="80%" width="80%"/></p>
<br />
Copy the public IP address and log in from Remote Desktop.
<p><img src="https://i.imgur.com/N8QNhwl.png" height="80%" width="80%"/></p>
<br />
In the search bar, type "Powershell". Click "run as Administrator".
<p><img src="https://i.imgur.com/kOGrsQF.png" height="80%" width="80%"/></p>
<br />
Ping the privte IP address of the Domain Controller by typing "ping 10.0.0.4".
<p><img src="https://i.imgur.com/mEV4pA1.png" height="80%" width="80%"/></p>
<br />
If everthing worked correctly, there will be 4 replies (the default amount of packets sent). Lost indicates if there are any issues.
<p><img src="https://i.imgur.com/bB7DDgg.png" height="80%" width="80%"/></p>
<br />
Type "ipconfig /all". This will show us the internet protocol for the client Virtual Machine.
<p><img src="https://i.imgur.com/iAdRhHE.png" height="80%" width="80%"/></p>
<br />
Under "DNS Servers", the Domain Controller's private IP address should show up.
<p><img src="https://i.imgur.com/aggBicO.png" height="80%" width="80%"/></p>
<br />

The client Virtual Machine is now connected to the Domain Controller!



<h2>Installing Active Directory</h2>

<p><img src="" height="80%" width="80%"/></p>
<br />

<p><img src="" height="80%" width="80%"/></p>
<br />

<p><img src="" height="80%" width="80%"/></p>
<br />

<p><img src="" height="80%" width="80%"/></p>
<br />
