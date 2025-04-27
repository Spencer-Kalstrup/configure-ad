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
- Create Domain Admin User
- Connect the Client to the Domain
- Setup Remote Desktop for Non-Administrative Users
- Create Additional Users



<h2>Creating and Configuring a Domain Controller in Azure</h2>
To create a domain controller, open Azure and click "Resource Groups".
<p><img src="https://i.imgur.com/IaDRU8l.png" height="80%" width="80%"/></p>
<br />
Click "Create".
<p><img src="https://i.imgur.com/AywQdZt.png" height="80%" width="80%"/></p>
<br />
Name the resource group "Active-Directory-Lab" and set the region to Canada Central. The region needs to be the same for the client virtual machine. Click create.
<p><img src="https://i.imgur.com/hLst4wt.png" height="80%" width="80%"/></p>
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
Inside the Domain Controller Server Manager, click "Add roles and features".
<p><img src="https://i.imgur.com/u0Hrzh9.png" height="80%" width="80%"/></p>
<br />
Click "Next".
<p><img src="https://i.imgur.com/x6RMFJ9.png" height="80%" width="80%"/></p>
<br />
Click "Role based or feature-based installation".
<p><img src="https://i.imgur.com/MgcJxzX.png" height="80%" width="80%"/></p>
<br />
Make sure the selected server is the private IP address of the Domain Controller, 10.0.0.4 in this case.
<p><img src="https://i.imgur.com/4Y1aPXH.png" height="80%" width="80%"/></p>
<br />
Check the box next to "Actice Directory Domain Service".
<p><img src="https://i.imgur.com/KHWChNa.png" height="80%" width="80%"/></p>
<br />
Click "Add Features".
<p><img src="https://i.imgur.com/lD0Bn0I.png" height="80%" width="80%"/></p>
<br />
Click "Next".
<p><img src="https://i.imgur.com/nkAnlfn.png" height="80%" width="80%"/></p>
<br />
Click "Next".
<p><img src="https://i.imgur.com/Sc8pSpB.png" height="80%" width="80%"/></p>
<br />
Click "Next".
<p><img src="https://i.imgur.com/ZqeDRJZ.png" height="80%" width="80%"/></p>
<br />
Check the box next to "Restart the destination server automatically if required". Click "Yes". Click "Install"
<p><img src="https://i.imgur.com/qlKfTIS.png" height="80%" width="80%"/></p>
<br />
Once the installation is completed, the Virtual Machine will restart.
<p><img src="https://i.imgur.com/Eg4kwpS.png" height="80%" width="80%"/></p>
<br />
After the Domain Controller restarts, log back in and click the flag icon in the top right corner.
<p><img src="https://i.imgur.com/9v5u03K.png" height="80%" width="80%"/></p>
<br />
Click "Promote this server to a domain controller".
<p><img src="https://i.imgur.com/Xvl265Y.png" height="80%" width="80%"/></p>
<br />
Click the circle next to "Add a new forest". For the "Root domain name", enter "mydomain.com". Click "Next".
<p><img src="https://i.imgur.com/dsx3t1e.png" height="80%" width="80%"/></p>
<br />
Create a password, for this lab we will use "Cyberlabe123!". Click "Next".
<p><img src="https://i.imgur.com/qzvPjCL.png" height="80%" width="80%"/></p>
<br />
The box next to "Create DNS Delegation" should NOT be marked. Click "Next".
<p><img src="https://i.imgur.com/TdXGklU.png" height="80%" width="80%"/></p>
<br />
The "NetBIOS domain name" should be MYDOMAIN. Click "Next".
<p><img src="https://i.imgur.com/mAjwMox.png" height="80%" width="80%"/></p>
<br />
Click "Next".
<p><img src="https://i.imgur.com/qfX6A2T.png" height="80%" width="80%"/></p>
<br />
Click "Next".
<p><img src="https://i.imgur.com/PBSjnUX.png" height="80%" width="80%"/></p>
<br />
Click "Install".
<p><img src="https://i.imgur.com/SigaqqN.png" height="80%" width="80%"/></p>
<br />
Restart Remote Desktop. When the login screen appears, it should say "User@Domain or Domain\Uer"
<p><img src="https://i.imgur.com/Kc55rOI.png" height="80%" width="80%"/></p>
<br />
Login using either "labuser@mydomain.com" or "mydomain.com\labuser"
<p><img src="https://i.imgur.com/xed9dv1.png" height="80%" width="80%"/></p>
<br />

The Domain Controller Active Directory is now Configured!



<h2>Connecting the Client to the Domain</h2>
While logged into the Domain Controller as "Jane Doe" or our Admin user, right click the windows icon and click "Windows Administrative Tools", then "Active Directory Users and Computers".
<p><img src="https://i.imgur.com/LoPFOoB.png" height ="80%" width="80%"/></p>
<br />
Right-click mydomain.com, hover over "New", click "Organizational Unit".
<p><img src="https://i.imgur.com/fTTJZKf.png" height ="80%" width="80%"/></p>
<br />
Enter "_EPLOYEES". Click "OK".
<p><img src="https://i.imgur.com/Y2SfONB.png" height ="80%" width="80%"/></p>
<br />
Repeat the process for and name the new unit "_ADMINS".
<p><img src="<p><img src="https://i.imgur.com/eXyE1DY.png" height ="80%" width="80%"/></p>
" height ="80%" width="80%"/></p>
<br />
Enter the new folder "_ADMINS".
<p><img src="https://i.imgur.com/NkbeCXs.png" height ="80%" width="80%"/></p>
<br />
Right-click the blank area, hover over new, click "User".
<p><img src="https://i.imgur.com/8MSXMRh.png" height ="80%" width="80%"/></p>
<br />
Create a new user for the domain. In this lab the user named "Jane Doe".
<p><img src="https://i.imgur.com/ClYxccj.png" height ="80%" width="80%"/></p>
<br />
In the "_ADMINS" folder, right click "Jane Doe". Click "Properties". 
<p><img src="https://i.imgur.com/HDWO4gT.png" height ="80%" width="80%"/></p>
<br />
Click the "Member Of" tab the click "Add".
<p><img src="https://i.imgur.com/Z7RSGJk.png" height ="80%" width="80%"/></p>
<br />
Type "Domain Admins". Click "Check Names". Click "OK".
<p><img src="https://i.imgur.com/S5Ry2C1.png" height ="80%" width="80%"/></p>
<br />
Click "Apply" then click "OK".
<p><img src="https://i.imgur.com/0FzefWy.png" height ="80%" width="80%"/></p>
<br />
Log off of the domain controller by pressing CTRL + R and typing "logoff".
<p><img src="https://i.imgur.com/Y4kXCgE.png" height ="80%" width="80%"/></p>
<br />
Log back into the domain controller with the new admin account.
<p><img src="https://i.imgur.com/9PnLudu.png" height ="80%" width="80%"/></p>
<br />
Log in to the Client virtual machine. Right-click the windows icon. Select "System".
<p><img src="https://i.imgur.com/clzsAeP.png" height ="80%" width="80%"/></p>
<br />
Scroll down and click "Rename this PC (advanced).
<p><img src="https://i.imgur.com/H5ZR1Jx.png" height ="80%" width="80%"/></p>
<br />
Click "Change".
<p><img src="https://i.imgur.com/T7IiiqC.png" height ="80%" width="80%"/></p>
<br />
Click the circle next to "Domain". Enter "mydomain.com". Click "OK".
<p><img src="https://i.imgur.com/iIlckIp.png" height ="80%" width="80%"/></p>
<br />
Enter the new admin account.
<p><img src="https://i.imgur.com/ZpbsmQ6.png" height ="80%" width="80%"/></p>
<br />
Close out of the windows to show the pop-up. Click "OK"
<p><img src="https://i.imgur.com/0I2JUEw.png" height ="80%" width="80%"/></p>
<br />
Click "OK"
<p><img src="https://i.imgur.com/OzB9O4j.png" height ="80%" width="80%"/></p>
<br />
Click "Restart Now"
<p><img src="https://i.imgur.com/udLAve8.png" height ="80%" width="80%"/></p>
<br />
After the Client Virtual Machine restarts, navigate to the domain controller and type "active directory users and computers" into the windows search bar. Open the application.
<p><img src="https://i.imgur.com/wq2lUvc.png" height ="80%" width="80%"/></p>
<br />
Click the drop box next to "mydomain.com". Client-1 should show up.
<p><img src="https://i.imgur.com/8muJvcg.png" height ="80%" width="80%"/></p>
<br />
Right-click "mydomain.com". Hover over "New", click "Organizational Unit".
<p><img src="https://i.imgur.com/u0b37BG.png" height ="80%" width="80%"/></p>
<br />
Name the new unit "_CLIENTS".
<p><img src="https://i.imgur.com/qiGfexa.png" height ="80%" width="80%"/></p>
<br />
Double-click "Computers". Click and drag "client-1" into the "_CLIENTS" organizational unit.
<p><img src="https://i.imgur.com/64M7GWK.png" height ="80%" width="80%"/></p>
<br />
Click "Yes".
<p><img src="https://i.imgur.com/aXGChXF.png" height ="80%" width="80%"/></p>
<br />
Right-click "mydomain.com". Click "Refresh".
<p><img src="https://i.imgur.com/bog8JSi.png" height ="80%" width="80%"/></p>
<br />

The Client is now connected to the Domain!



<h2>Setting Up Remote Desktop for Non-Administrative Users</h2>
<br />
Log in to the client as the new admin.
<p><img src="https://i.imgur.com/KvHGbs2.png" height ="80%" width="80%"/></p>
<br />
Right-click the windows icon. Click "System"
<p><img src="https://i.imgur.com/b3rCAZr.png" height ="80%" width="80%"/></p>
<br />
Scroll down and click "Remote desktop"
<p><img src="https://i.imgur.com/fptWJmw.png" height ="80%" width="80%"/></p>
<br />
Click "Select users that can remotely access this PC".
<p><img src="https://i.imgur.com/sBzytgM.png" height ="80%" width="80%"/></p>
<br />
Click "Add"
<p><img src="https://i.imgur.com/wGFZ0XN.png" height ="80%" width="80%"/></p>
<br />
Type "Domain Users". Click "Check names" then "OK".
<p><img src="https://i.imgur.com/bmbr0UF.png" height ="80%" width="80%"/></p>
<br />
Click "OK"
<p><img src="https://i.imgur.com/07REEJf.png" height ="80%" width="80%"/></p>
<br />

Remote Desktop is now ready! We can also do this process much faster using group updates. I will go over this in the future.



<h2>Creating Additional Users</h2>

Log in to the domain controller as an admin. Type "Powershell" in the search bar. Right-click "Windows Powershell ISE". Click "Run as administrator".
<p><img src="https://i.imgur.com/nwolDnR.png" height ="80%" width="80%"/></p>
<br />
Click "Yes"
<p><img src="https://i.imgur.com/IqZtByw.png" height ="80%" width="80%"/></p>
<br />
Click the icon that creates a new file
<p><img src="https://i.imgur.com/VWQT2lK.png" height ="80%" width="80%"/></p>
<br />
Click the save icon.
<p><img src="https://i.imgur.com/RG5rLM7.png" height ="80%" width="80%"/></p>
<br />
Save the file to the desktop and name it C"reate-users".
<p><img src="https://i.imgur.com/lYtTCLF.png" height ="80%" width="80%"/></p>
<br />
Copy <a href="https://github.com/Spencer-Kalstrup/AD-Gen-Names-Create-Users/blob/main/README.md">this script</a> into the application. Click the "run script" icon and click "OK".
<p><img src="https://i.imgur.com/yew73ms.png" height ="80%" width="80%"/></p>
<br />
Observe the new users being created.
<p><img src="https://i.imgur.com/EXsQEX1.png" height ="80%" width="80%"/></p>
<br />
Press CTRL + "R" and type "dsa.msc" to open Active Directory Users and Computers.
<p><img src="https://i.imgur.com/AiJgeuT.png" height ="80%" width="80%"/></p>
<br />
Double-click "_EMPLOYEES". Observe the new users and select one to login to the client virtual machine. For this lab the account "hiv.kug" will be used.
<p><img src="https://i.imgur.com/lAMrwLW.png" height ="80%" width="80%"/></p>
<br />
Enter the username using the correct domain formatting.
<p><img src="https://i.imgur.com/ZRk8Z0Q.png" height ="80%" width="80%"/></p>
<br />
Verify the account user by clicking the windows icon then clicking the profile icon.
<p><img src="https://i.imgur.com/4h8fVpT.jpeg" height ="80%" width="80%"/></p>
<br />

The user has been successfully created!



