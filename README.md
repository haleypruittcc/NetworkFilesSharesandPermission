<p align="center">
<img src="https://wiki.hornbill.com/images/d/d6/Activedirectory_logo.png"/>
</p>

<h1>Active Directory</h1>
Active Directory is a software bulit and maintained by Microsoft that centrally manage thousands of user accounts in a single place, allows you to manage devices on a large scale, and provieds a way to control access to resource on a large scale. This tutorial we're going to be learning how to deploying active directtory and creating useres.
<h2>Tools and Requirements used </h2>

- Computer with Internet Connection
- Microsoft Azure
- Vitural Machines (Window Server 2022 and Windows 10)
- Remote Desktop
- Active Directory
<h2>Configuration Steps</h2>


<h3>Step 1: Create Resource Group and Virtual Machine </h3>


<p align="center">
<img src="" height="80%" width="80%" alt="Azure Free Account"/>
  


- First going to create your Virtual Machine by naming (Windows Server 2022) "DC-1" and naming the other one "Client-1"
   - Make sure that both of your VMs are in the same Vnet (you can check the topology with Networker Watcher. If you don't know how , you can learn and following this tutorial [here](https://github.com/haleypruittcc/ResourcegroupandHelloworld).


<h3>Step 2: Ensure Connectivity between the client and Domain Controller </h3>

<p align="center">
<img src="https://i.imgur.com/5xs5hdE.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- Login to Client-1 with Remote Desktop and ping "-t ip address" 
- Login to the Domain Controller and enable ICMPv4 on the local windows Firewall.
- Go back to Client-1 to see the ping succeed.



<h3>Step 3: Install Active Directory </h3>

<p align="center">
<img src="" height="70%" width="70%" alt="Azure Free Account"/> <img src="" height="70%" width="70%" alt="Azure Free Services"/>
</p>

- First, login to "DC-01" on remote desktop and install Active Directory Domain Services
- Promote as a DC-1: Setup a new forest as "mydomain.com" or the name of your chose but make sure to remember it.
- Restart and then log back to "DC-1" on remote desktop by the user name you create earlier.


<h3>Step 4: Create an Admin and Normal User Account in AD </h3>

<p align="center">
<img src="https://i.imgur.com/5xs5hdE.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- In Active Dircetory Users and Computers (ADUC), create an Organizational Unit (OU) called "_EMPLOYEES" 
- Next, Create a new OU named "_ADMINS" 
- Create a new employees named of chose example: "Haley Pruitt" (same password as eariler) with username of "haley_admin".
- Add "haley_admin" to the "Domain Admins" Security Group.
- Log out the Remote Desktop connection to DC-1 and back in as "mydomain.com\haley_admin"
- User haley_admin as domain account for now on.



<h3>Step 5: Join Client-1 to your domain (mydomain.com) </h3>
 
 <p align="center">
<img src="https://i.imgur.com/ZemzOKX.png" height="70%" width="70%" alt="Azure Free Account"/> <img src="https://i.imgur.com/Z01V8dO.png" height="70%" width="70%" alt="Azure Free Services"/> <img src="https://i.imgur.com/r71MgMU.png" height="70%" width="70%" alt="Azure Free Account"/> [<img src="https://i.imgur.com/kSumXSD.png" height="70%" width="70%" alt="Azure Free Account"/>] <img src="https://i.imgur.com/gSULz5Z.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>
 
- From the Azure Portal, set Client-1's DNS settings to the DC'S Private IP address.
- From the Azure Portal, restart Client-1 
- Login to Client(Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers(ADUC) inside the "Computers" container on the root of the domain.
- Create a new OU names "_CLIENTS" and drag Client-1 into there.



<h3>Step 5: Setup Remote Desktop for non-administrative users on Client-1 </h3>


<p align="center">
<img src="https://i.imgur.com/I85PIqP.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>
 
- Log into Client-1 as mydomain.com\haley_admin and open system properties,
- Click "Remote Desktop"
- Allow "domain users" access to remote desktop
- You can now log into Client-1 as a normal, non-administrative user now.

  <h3>Step 6:Create a bunch of additional users and attempt to log into client-1 with one of the users </h3>
  
- Login to DC-1 as haley_admin
- Open Powershell_ise as an administrator
- Create a new File and paste the contents of the script into it by getting it [here](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
- Run script and observe the accounts being created
   - When finished, open ADUC and observe the accounts in the appropriate OU.
- Now, attempt to log into Client-1 with one of the accounts( Make sure to take note of the password in the script)
  
  



