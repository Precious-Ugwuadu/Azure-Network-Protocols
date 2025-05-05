# Azure-Network-Protocols
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

-  Set Up Virtual Machines
-  Capture ICMP Traffic
- Configure Network Security Group (NSG) Rules
- Observe SSH, DHCP, DNS, and RDP Traffic

<h2>Actions and Observations</h2>

<p>  
  
  ![image](https://github.com/user-attachments/assets/4b874336-dfc1-4224-8540-6d53e71b6622)

  ![image](https://github.com/user-attachments/assets/2f5f5b56-d179-45d7-8bfd-ebc9c541f03f)

  ![image](https://github.com/user-attachments/assets/15668165-073f-4015-9a48-57263ea4277a)

   
</p>
<p>
You can start by creating a Resource Group to organize your resources.
Create a Windows 10 VM and allow it to set up a new Virtual Network and Subnet.
Next, create a Linux (Ubuntu) VM using the same Resource Group and the same Virtual Network/Subnet.
Use a username and password for Linux authentication so both VMs can connect on the same network.
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/2ce95ba5-7e02-4e54-96f5-e86ff3374bc2)

Next, we will use Remote Desktop to connect to our VM by navigating to the VM in the Azure Portal, copying its public IP address, and signing in through the Remote Desktop application.  


![image](https://github.com/user-attachments/assets/d65afa4d-fb45-4d1b-bdaa-0fa50c4fad7e)

</p>
<p>
Next, we will install Wireshark to serve as our protocol analyzer. It will help us examine network traffic  and observe communication between the two VMS, allowing us to view incoming and outgoing traffic on our VM.
  
</p>
<br />



<p>
</p>

<p>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
