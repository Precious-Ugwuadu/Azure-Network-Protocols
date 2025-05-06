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

I useed Remote Desktop to connect to our VM by navigating to the VM in the Azure Portal, copying its public IP address, and signing in through the Remote Desktop application.  


![image](https://github.com/user-attachments/assets/d65afa4d-fb45-4d1b-bdaa-0fa50c4fad7e)

</p>
<p>
Next, I installed Wireshark to serve as our protocol analyzer. It will help us examine network traffic  and observe communication between the two VMS, allowing us to view incoming and outgoing traffic on our VM.
  
</p>
<br />


![image](https://github.com/user-attachments/assets/14cd6ddd-6d85-44b2-96ca-1a8714d60fbe)


At this stage, I started packet capturing by highlighting Ethernet and clicking on the Wireshark icon to see the network traffic at the back end. So, what I am doing here is inspecting the traffic in Windows VM1. 

![image](https://github.com/user-attachments/assets/6434bd01-08ef-4ce6-b490-b72efcf5ad6e)

Next, I typed ICMP in the search bar to filter for ICMP traffic. ICMP is what "ping" uses to test connectivity between devices, and this will show me only ICMP traffic. Furthermore, I will go to the Azure portal and copy Linux-VM private IP address, open PowerShell "ping" VM2, and i was able to see ICMP traffic in Wireshark and inspect it. the screen shoot you see above is a request and reply from Linux and Windows computers.  

![image](https://github.com/user-attachments/assets/812eacbc-b3f9-40d4-82bc-5f522019e730)

![image](https://github.com/user-attachments/assets/1e7932ce-fd73-4773-b471-85215341f48d)

![image](https://github.com/user-attachments/assets/0acb4245-1969-46d8-959e-9960f003bb23)





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
