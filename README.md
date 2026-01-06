<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines. <p></p>
Active Directory is a software built and maintained by Microsoft that centrally manage thousands of user accounts in a single place. This allows you to manage devices on a large scale.
<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Setting up and configuring Azure Virtual Machines for Active Directory</h2>

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/cc35d549-7d82-447f-a98f-ac0d0a9aea88" />
</p>
<p>
I deployed DC-1 VM which is going to be the domain controller in the Active Directory lab. </p>
This domain controller manages user accounts, authentication, and security policies for the network domain. </p>In this setup, DC-1 will also act as the DNS server, which is essential for your client VM (Client-1) to find and join the domain.
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/9ba9f433-41d0-43fd-a2b1-3819c66de4e5" />
</p>
<p>
Here, we ensured this vm is on the same vnet.</p>
I created the vnet to provide a private, isolated network in Azure where your VMs (like DC-1 and Client-1) can communicate securely with each other. </p>
The vnet ensures both VMs are on the same network segment, allowing things like Active Directory domain joins and local network communication, just like computers on the same physical local network in an actual business environment.
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/1cf39314-a0f1-4677-b83c-7fedb7af41de" />
</p>
<p>
Then I created Client-1 VM on the same vnet. </p>
Client-1 is a virtual machine that acts as a domain-joined client computer in your lab. Its main purpose is to simulate a typical company workstation that connects to the domain managed by DC-1.  </p>
  <ins>I will use Client-1 to:</ins>

   - Join the domain controlled by DC-1.
   - Log in with domain user accounts created in Active Directory.
   - Test domain policies, authentication, and permissions as you would with real users' computers in a business environment.
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/7b8c4980-d9bc-4fdb-adcb-8650e3daf95a" />

</p>
<p>
I've changed DC-1’s private IP from dynamic to static so it would never change, even if the VM is restarted. </p>
  <ins>This is important because: </ins>

   - Client-1 (and other devices) need a consistent IP to find and use DC-1 as the DNS server and domain controller.
   - If DC-1’s IP changed, connections, DNS resolution, and domain join operations could fail.
   - Setting a static IP ensures reliable communication between devices in your lab network.
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/2e08329f-f47f-4181-ace9-19de670e7c3d" />
</p>
<p>
Now to configure DNS to dc-1. </p>
  I configured the DNS on Client-1 to point to DC-1 because DC-1 acts as both the domain controller and DNS server. </p>
  This lets Client-1 find and join the Active Directory domain, since only DC-1 knows about my lab domain (not public DNS servers). </p> Without this, Client-1 wouldn't locate the domain controller or join the domain.
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/05b781f7-dfac-4c6f-a829-45e63b05bcbd" /> <img width="600" alt="image" src="https://github.com/user-attachments/assets/6d913603-0bae-477b-91a9-96df1f35fe7c" />

</p>
<p>
Next, I want to make sure that my lab’s network and domain configuration are set up correctly.</p>
  To do this, I logged into Client-1 and pinged DC-1's private IP to verify if Client-1 can communicate with DC-1 across the network to verify network connectivity.</p>
  Then I used ipconfig to check DNS settings to confirmed Client-1 is using DC-1 as its DNS server, ensuring it can find and join the domain.</p>
</p>
<br />

<h2>Setting up Active Directory to add admins and users.</h2>

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/4ce98c8a-da61-45dd-9102-a31903bb6f2d" />
</p>
<p>
Now I am going to install the Active Directory services. </p>
First, log in to DC-1 and look for Server Manager in the windows start.</p>
  Click add roles and features, then click next until you to get to services and choose Active Directory Domain Services and install it.

</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/bb621a6a-5b06-4803-ba24-fa93b5fa4686" />
</p>
<p>
Now to promote DC-1 to domain controller. </p>
  After installation, in Server Manager, look for a notification flag. When you hover over it, it should say, ("promote this server to a domain controller"). </p>
  Click it and choose Add a new forest. </p>
  Then set the domain name to mydomain.com </p>
  Next, Set a directory services restore mode password. </p>
Proceed through the wizard and click Install then exit out of DC-1 and restart the VM </p>
Now I can log back in as a domain user which is mydomain.com\labuser 
</p>
<br />

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/deb2a9c5-adbc-4646-bb69-7a1f2c9be582" /> <img width="400" alt="image" src="https://github.com/user-attachments/assets/931107ca-0fbc-494f-8411-5238e2bbcae3" />
<img width="400" alt="image" src="https://github.com/user-attachments/assets/42559932-4371-45a0-8d9f-e11801156cd1" />
</p>
<p>
Now to create a Domain Admin user within the domain.</p>
I'm creating a domain admin so I could have a user account with full administrative rights over the entire domain. In this account, I can manage all users, computers, and security settings and configure group policies, permissions, and access.</p>
To do this, first, look for and open Active Directory Users and Computers in the windows menu. Click Start > Administrative Tools > Active Directory Users and Computers.</p>
<ins>Next, Create "_EMPLOYEES" Organizational Unit(OU)</ins> </p>
   - In the left pane, right-click your domain name(mydomain.com) </p>
   - Select New > Organizational Unit. </p>
   - Enter _EMPLOYEES (with the underscore). </p>
   - Click OK. </p>
Then Create _ADMINS using the same steps above.
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/c734688d-da52-4845-825b-a57395b24d53" />
</p>
<p>
Now I'm going to create a new user called Jane Doe to give full admin rights for managing the domain. </p>
   - In Active Directory Users and Computers (ADUC), right-click the _ADMINS OU. </p>
   - Choose New > User. </p>
   - Enter the full name “Jane Doe” and username “jane_admin”. </p>
   - Set the password and finish. </p>
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/0e68de8f-049f-4c56-980c-34d86d3808b4" />
</p>
<p>
<ins>Then, add jane_admin to the “Domain Admins” group: </ins>

   - Right-click the jane_admin user > Properties.
   - Go to the Member Of tab.
   - Click Add, search for Domain Admins, and add it.
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/86c3b8a1-e5bf-45eb-8db8-58ebc8b2a8da" /> 
</p>
<p>
Next, Login to Client-1 as local admin.
<ins>Then join Client-1 to the domain</ins>
  
   - Right-click Start and select System.
   - Click Rename this PC (Advanced) > Change.
   - Under Member of, select Domain and enter your domain(mydomain.com).
   - Enter the credentials of a domain admin(mydomain.com\jane_admin).
   - Restart Client-1 when prompted. </p>
I joined the domain. Because we configured the dns settings to set the client-1's IP address to be the same as dc-1's IP address, it was able to locate the domain controller for mydomain.com. 
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/b4823c58-c32e-4ccb-887b-7f05bef446f8" />
</p>
<p>
Then go back to DC-1 and open Active Directory Users and Computers. </p>
Look under the Computers container to confirm "Client-1" is listed. </p>
Create a "_CLIENTS" OU and move Client-1. </p>

**Why create a "_CLIENT" OU?** </p>
The _CLIENTS OU is used to keep clients together and to make management easier so that Group Policies (GPOs) can be applied specifically to the _CLIENTS OU, targeting only client machines. </p>
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/2a70dc62-ac11-44d6-8d01-24f365918625" />
</p>
<p>

</p>
<br />

<p>
<img width="1275" height="857" alt="image" src="https://github.com/user-attachments/assets/49e526e0-0d72-45a1-8485-3e7a56f0b404" />
</p>
<p>
Within powershell, I logged in as admin to create 1000 users to our domain
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
