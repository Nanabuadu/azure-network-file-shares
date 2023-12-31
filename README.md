<p align="center">
<img src="https://i.imgur.com/HPzIb4m.png" alt="Traffic Examination"/>
</p>

<h1>Network File Share and Permissions</h1>
In this tutorial, we share out resources over the network and create file shares to allow Read, Write, or Deny access to individual users or groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022

<h2>High-Level Steps</h2>

- Create some sample file shares with various permissions
- Attempt to access file shares as a normal user

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/BgKuK35.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the previous tutorial on Active Directory, we created a Windows server virtual machine and named it DC-1. We also created a Windows 10 virtual machine and named it Client-1. inside DC-1, we created a domain admin (koby.charis) and a bunch of non-administrative users. for this tutorial, we will log in to DC-1 as a domain admin (koby.charis) and Client-1 as a non-administrative user.
</p>
<br />

<p>
<img src="https://i.imgur.com/h7ZzMYl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create 4 folders on C:\drive on DC-1 ("read-access", "write access", "no-access", "accounting")
</p>
<br />

<p>
<img src="https://i.imgur.com/Tm5Fuqd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set "Read" permission to the "read-access" folder for Domain Users: Right-click the "read-access" folder -> Properties -> Sharing -> Share -> Type domain users in the box -> click on "Add" -> Change "Permission Level" to "Read" -> Share.
</p>
<br />

<p>
<img src="https://i.imgur.com/e8p1Vvt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set "Read/Write" permission to the "write-access" folder for Domain Users: Right-click the "write-access" folder -> Properties -> Sharing -> Share -> Type domain users in the box -> click on "Add" -> Change "Permission Level" to "Read/write" -> Share.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZyoydAS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set "Read/Write" permission to the "no-access" folder for Domain Admins: Right-click the "no-access" folder -> Properties -> Sharing -> Share -> Type Domain Admins in the box -> click on "Add" -> Change "Permission Level" to "Read/write" -> Share.
</p>
<br />

<p>
<img src="https://i.imgur.com/tL3xIiQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, access the shared folders as a Domain User: Start -> Run -> type \\dc-1
</p>
<br />

<p>
<img src="https://i.imgur.com/642mxa8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Attempt to open the read-access folder and see it succeed. However, because we set "Read" permission to the folder, any attempt to perform any action in the folder will fail. 
</p>
<br />

<p>
<img src="https://i.imgur.com/afu2eNr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Attempt to open the write-access folder and see it succeed. Also, attempt to create a text document file (Right-click -> New -> Text Document). the file will be created successfully because we set "Read/Write" permission to the folder, any attempt to perform any action in the folder will be successful.
</p>
<br />

<p>
<img src="https://i.imgur.com/VDhUsl0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Attempt to open the no-access folder and see it fail. We set "Read/Write" permission for "Domain Admins", in effect, Domain Users can not have access to the folder. Note that the name of the folder(no-access) has no bearing on this outcome.
</p>
<br />
