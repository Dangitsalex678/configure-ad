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

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity Between the Client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account
- Join Client-1 to the Domain
- Setup Remote Desktop for Non-Administrative Users on Client-1
- Create Random Users and Attempt to Log into Client-1

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/0NduLQU.png" height="80%" width="80%" alt="Creating Resource Groups in Azure"/>
</p>
<p>
<b>- Create a Virtual Machine running Windows Server 2022 Datacenter named "Client-1"
</p>- Create another Virtual Machine running Windows 10 Pro named "DC-1"
</p>
<br />

<p>
<img src="https://i.imgur.com/AG2twLQ.png" height="80%" width="80%" alt="Setting DC-1 Private IP to Static"/>
</p>
<p>
<b>- Navigate to the DC-1 Virtual Machine and select Networking under settings
</p>- Click on the Network Interface (NIC)
</p>- Click on IP Configurations
</p>- Click on the Private IP Address and set it to Static
</p>
<br />

<p>
<img src="https://i.imgur.com/n1CkOLh.png" height="80%" width="80%" alt="Pinging Virtual Machines"/>
</p>
<p>
<b>- Login into Client-1 and ping DC-1 with ping -t
</p>- Login to the Domain Controller and enable ICMPv4 on the local windows firewall
</p>- Log back into Client-1 to see if the pings are successfull
</p>
<br />

<p>
<img src="https://i.imgur.com/BabNW32.png" height="80%" width="80%" alt="Installing Active Directory"/>
</p>
<p>
<b>- Open up Server Manager on DC-1 
</p>- On the Dashboard, click on Add Roles and Features
</p>- Keep clicking next until you reach Server Roles
</p>- Click to enable "Active Directory Domain Services"
</p>- Click Add Features
</p>- Finish the installation
</p>
<br />

<p>
<img src="https://i.imgur.com/gWSEE50.png" height="80%" width="80%" alt="Finishing Installing Active Directory"/>
</p>
<p>
<b>- On the Server Manager Dashboard, click the yellow flag near the upper right corner
</p>- Click on "Promote this server to a domain server"
</p>- Create a new forest and name the domain to what ever you want .com
</p>
<br />

<p>
<img src="https://i.imgur.com/qfWAsPD.png" height="80%" width="80%" alt="Creating Admin and Normal Users"/>
</p>
<p>
<b>- Navigate to the Active Directory Users and Computers
</p>- Right click your domain and create a new Organizational Unit
</p>- Create two Organizational Units and name them "Employees" and "Admins"
</p>
<br />

<p>
<img src="https://i.imgur.com/LBPM5g3.png" height="80%" width="80%" alt="Assigning Groups"/>
</p>
<p>
<b>- Right click and add a new user into the Admins Group
</p>- Name the new user Jane Doe with the Username "jane_admin"
</p>- Click Next and uncheck "User must change password on next login"
</p>- Right click the new user and select Properties
</p>- Navigate down to the Member Of Tab
</p>- Type down Domain in the object name
</p>- Select "Domain Admins"
</p>- Press OK and Apply
</p>- Logoff and Log back in
</p> 
<br />

<p>
<img src="https://i.imgur.com/y4QxZ6G.png" height="80%" width="80%" alt="Assigning DNS Server"/>
</p>
<p>
<b>- Go to Azure Portal and copy DC-1 Private IP
</p>- Then select Client-1
</p>- Under settings click on Networking and click on the Virtual NIC
</p>- Under settings click on DNS Servers
</p>- Select Custom DNS Server and paste the Private IP
</p>- Click on Save
</p>- Restart Client-1
</p> 
<br />

<p>
<img src="https://i.imgur.com/gMIGCEi.png" height="80%" width="80%" alt="Adding Client-1 to the Domain"/>
</p>
<p>
<b>- Login to Client-1 with your Admin Account
</p>- Right click the Start Button and select System
</p>- Click "Rename this PC"
</p>- Click the Change button
</p>- Enter the custom domain from earlier
</p>- When prompted, login with Jane Doe Admin that was created earlier
</p> 
<br />


<p>
<img src="https://i.imgur.com/ogUZCiO.png" height="80%" width="80%" alt="Allowing Domain Access"/>
</p>
<p>
<b>- Login to Client-1 with Jane Doe Admin Account
</p>- Right click the Start Button and select System
</p>- Click "Remote Desktop"
</p>- Click on "Select users that can remotely access the PC
</p>- Enter "Domain Users" to allows all users to access the PC
</p>- 
</p> 
<br />

<p>
<img src="https://i.imgur.com/ogUZCiO.png" height="80%" width="80%" alt="Allowing Domain Access"/>
</p>
<p>
<b>- Login into DC-1 with jane_admin
</p>- Open PowerShell_ise as an administrator
</p>- Click "Remote Desktop"
</p>- Click on "Select users that can remotely access the PC
</p>- Enter "Domain Users" to allows all users to access the PC
</p>- 
</p> 
<br />
