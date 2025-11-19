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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/cc35d549-7d82-447f-a98f-ac0d0a9aea88" />
</p>
<p>
dc-1 created
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/9ba9f433-41d0-43fd-a2b1-3819c66de4e5" />
</p>
<p>
Here, we ensured this vm is on the same vnet
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/1cf39314-a0f1-4677-b83c-7fedb7af41de" />
</p>
<p>
Client 1 vm created
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/7b8c4980-d9bc-4fdb-adcb-8650e3daf95a" />

</p>
<p>
Dynamic to static
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/2e08329f-f47f-4181-ace9-19de670e7c3d" />
</p>
<p>
configured dns to dc-1
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/05b781f7-dfac-4c6f-a829-45e63b05bcbd" /> <img width="600" alt="image" src="https://github.com/user-attachments/assets/6d913603-0bae-477b-91a9-96df1f35fe7c" />

</p>
<p>
Pinged 10.0.0.4
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/4ce98c8a-da61-45dd-9102-a31903bb6f2d" />
</p>
<p>
Instaled AD
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/bb621a6a-5b06-4803-ba24-fa93b5fa4686" />
</p>
<p>
Promoted to domain controller
</p>
<br />

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/deb2a9c5-adbc-4646-bb69-7a1f2c9be582" /> <img width="400" alt="image" src="https://github.com/user-attachments/assets/931107ca-0fbc-494f-8411-5238e2bbcae3" />
<img width="400" alt="image" src="https://github.com/user-attachments/assets/42559932-4371-45a0-8d9f-e11801156cd1" />

</p>
<p>
OUs admin employees
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/c734688d-da52-4845-825b-a57395b24d53" />
</p>
<p>
JANE admin
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/0e68de8f-049f-4c56-980c-34d86d3808b4" />
</p>
<p>
domain admins
</p>
<br />

<p>
<img width="600" alt="image" src="https://github.com/user-attachments/assets/86c3b8a1-e5bf-45eb-8db8-58ebc8b2a8da" /> <img width="600" alt="image" src="https://github.com/user-attachments/assets/b4823c58-c32e-4ccb-887b-7f05bef446f8" />
</p>
<p>
Joined domain. Because we configured the dns settings to set the client-1's ip address to be the same as dc-1's ip address, it was able to locate the domain controller for mydomain.com. Then we logged in as Jane, an admin, and created a new organizational unit to put client-1 in.
</p>
<br />

<p>
<img width="1243" height="863" alt="image" src="https://github.com/user-attachments/assets/2a70dc62-ac11-44d6-8d01-24f365918625" />
</p>
<p>
Domain users to connect
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
