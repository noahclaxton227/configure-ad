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

- Step 1: Create Domain Controller VM and Client VM
- Step 2: Access Local Firewall to Ensure Connectivity
- Step 3: Install Active Directory (AD) and Create New Forest
- Step 4: Create Admin and Normal User on AD
- Step 5: Setup Remote Desktop for non-admin Users
- Step 6: Log Into Client-1 with New Account

<h2>Deployment and Configuration Steps</h2>

<p>
  
![image](https://github.com/noahclaxton227/configure-ad/assets/150629711/14df55a9-7042-48d3-8045-92281bcb632a)

</p>
<p>
In this section, both a Domain Controller VM (DC-1) and Client  VM (Client-1) are created. The NIC private IP of DC-1 is also set to static in order to keep the IP address the same, so the client can always access the domain. 
</p>
<br />

<p>
  
![image](https://github.com/noahclaxton227/configure-ad/assets/150629711/a928313e-da55-4ffe-8ff2-cd9b8254efd3)

</p>
<p>
When attempting to ping DC-1 from Client-1, we recieve a "request timed out" message. To fix this, ICMPv4 under DC-1's local firewall had to be enabled, as ping runs the protocol ICMP.  
</p>
<br />

<p>
  
![image](https://github.com/noahclaxton227/configure-ad/assets/150629711/0c34eacc-491d-4a0d-abba-99476d280cf7)

</p>
<p>
Next, Active Directory is installed on the Server Manager. Open up Server Manager --> Add Roles --> Install Active Directory --> Promote as a Domain Controller --> Setup New Forest. Then we name the DC mydomain.com.  
</p>
<br />

<p>
  
![image](https://github.com/noahclaxton227/configure-ad/assets/150629711/adefc5d7-ddcc-435c-b7ef-7e1a165bb7e1)

</p>
<p>
The next goal is to create an admin in Active Directory. Under the "_EMPLOYEES" tab, Jane will represent be the new employee, while Jane will also get admin access. The additional step shown above is where Jane actually recieves the admin powers. Just placing her into the admin OU doesn't grant her those abilities, only by right clicking --> properties --> "member of", does she actually become an admin. 
</p>
<br />

<p>
  
![image](https://github.com/noahclaxton227/configure-ad/assets/150629711/b4a54d11-4e8f-4b6b-9ba1-01cbb2d6532c)

</p>
<p>
Non-administrative users also need Remote Desktop access in order to log into the Domain from any "integrated" computer. Normally, one would do this with a Group Policy, which allows one to change many devices at once, but not in this specific case. 
</p>
<br />

<p>
  
![image](https://github.com/noahclaxton227/configure-ad/assets/150629711/2c28f9aa-e006-4209-a3ae-183dd7455062)

</p>
<p>
In between these last two images, we formed many new users in PowerShell_ise in order to test whether or not our intergrating between systems was successful. As seen above, the operation was successful, as Mr. Bog Fer was able to log into Client-1 using mydomain.com\bog.fer, meaning our Active Directory is functional!
</p>
<br />

