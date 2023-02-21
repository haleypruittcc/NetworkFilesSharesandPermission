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
<h2>Network File shares and Permissions</h2>


<h3>Step 1: Create some sample file shares with variuos permissions </h3>


<p align="center">
<img src="https://i.imgur.com/3Sw6wOh.png" height="80%" width="80%" alt="Azure Free Account"/>
  
- Connect/log into DC-1 as your domain admin account (mydomain.com\haley_admin)
- Connect/log into Client-1 as a normal user (mydomain\<someuser>)
- On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
- Set the following permissions (share the folder) for the “Domain Users” group:
    - Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
    - Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
    - Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
      - (Skip Cybersecurity for now)




<h3>Step 2:Attempt to access file shares as a normal user  </h3>

<p align="center">
<img src="https://i.imgur.com/yK9Umup.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- On Client-1, navigate to the shared folder (start, run, \\dc-1)
- Try to access the folders you just created.
    - Which folders can you access? 
    - Which folders can you create stuff in? Does it make sense?




  
<h3>Step 3: Create an “Cybersecurity” Security Group, assign permissions, an test access
 </h3>

<p align="center">
<img src="https://i.imgur.com/DyS36We.png" height="70%" width="70%" alt="Azure Free Account"/> <img src="https://i.imgur.com/R3SppZy.png" height="70%" width="70%" alt="Azure Free Services"/>
</p>

<p align="center">
<img src="https://i.imgur.com/3Sw6wOh.png" height="70%" width="70%" alt="Azure Free Account"/> 
</p>

- Go back to DC-1, in Active Directory 
    - Create a security group called “Cybersecurity” , Make an folder of Organizational Units " _Security_Groups" by right click -> Groups-> Cybersecurity-> Security-> Press ok -> cybersecurity -> members-> Add "username" of your chose -> Apply -> Ok.
    
- On the “cybersecuirty” folder you created earlier, set the following permissions:
    - Folder: “Cybersecurity”, Group: “Cybersecurity”, Permissions: “Read/Write”
- On Client-1, as  <someuser>, try to access the accountants folder. 
      - It should fail. 
- Log out of Client-1 as  <someuser>
- On DC-1, make <someuser> a member of the “Cybersecurity”  Security Group
- Sign back into Client-1 as <someuser> and try to access the “Cybersecurity” share in \\DC-1\ 
      - Does it work now?

🎉Congratulations! You are finally done with Active Directory, DNS, Network Files shares and permissions🎉

