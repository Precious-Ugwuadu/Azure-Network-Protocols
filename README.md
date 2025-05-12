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


At this stage, I began packet capturing by selecting the Ethernet interface and clicking the Wireshark icon to monitor network traffic in the background. Essentially, I am inspecting the traffic on the Windows VM1. 

![image](https://github.com/user-attachments/assets/6434bd01-08ef-4ce6-b490-b72efcf5ad6e)

Next, I typed ICMP in the search bar to filter for ICMP traffic. ICMP is what "ping" uses to test connectivity between devices, and this will show me only ICMP traffic. Furthermore, I will go to the Azure portal and copy the Linux-VM private IP address, open PowerShell "ping" VM2, and I will be able to see ICMP traffic in Wireshark and inspect it. The screenshot above shows the request and reply received from Linux and Windows computers.  

Filtering helps me isolate and view specific network traffic. 

![image](https://github.com/user-attachments/assets/80da13ea-a516-48bf-a34a-d20d53c54d74)

Next, I will configure a firewall (this will help me get a good intuition of what’s happening in the background). First, I’ll initiate a nonstop ping from the Linux VM to the Ubuntu VM by typing "ping 10.0.0.5 -t" in PowerShell, and this will keep pinging continuously.

![image](https://github.com/user-attachments/assets/812eacbc-b3f9-40d4-82bc-5f522019e730)

Next, I will open the network Firewall "Ubuntu VM" and disable incoming ICMP traffic. I will configure the Linux-VM cloud Firewall and tell it to block all incoming ping traffic. 

HOW DO I DO THIS?

 - Go to the Azure Portal

 - Search for “Virtual Machines”

 - Select your Linux VM from the list.

 - In the Linux-VM menu, scroll down and click “Networking.”

 - Under Network Settings, find “Network Security Group” and click on the link linux-vm-nsg. This is the firewall for your Linux VM.

 - In the NSG (Network Security Group) menu, click on “Inbound security rules.”

 - Click the “Add” button to create a new rule.

I set the Action to deny, set priority to 290 to put it above 300, and 290 will be evaluated first. 

   
![image](https://github.com/user-attachments/assets/1e7932ce-fd73-4773-b471-85215341f48d)

With the above rules set, ICMP traffic from any source will be denied. Once the rule takes effect, it will start timing out


![image](https://github.com/user-attachments/assets/0acb4245-1969-46d8-959e-9960f003bb23)

While observing Wireshark, I stopped seeing requests and replies, and all I could see were requests because no response was found; the Firewall blocked them out. If I go back and delete the "Deny" rule, it will start allowing the replies to happen again. Type Ctrl-C to stop the ping activity. 

![image](https://github.com/user-attachments/assets/f915ed7c-4f83-47e3-b976-84b8b668194e)





<p>
</p>

<p>

<p>
![image](https://github.com/user-attachments/assets/ad9de5f0-ac1b-4ae5-b06f-d6146a65ea2a)
  
![image](https://github.com/user-attachments/assets/d0327954-eb86-4276-9875-d188712285bd) 

![image](https://github.com/user-attachments/assets/a88b15ee-6154-4591-a2c9-1aae0ddf8fcf)

![image](https://github.com/user-attachments/assets/f287784e-73d0-45ff-a257-27a34bf8eecd)

![image](https://github.com/user-attachments/assets/c4a9b033-378a-4975-b8a6-a4877d5d9238)



</p>
<p>


</p>
<br />
