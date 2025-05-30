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
To begin, i started by creating a Resource Group to organize my resources.
Create a Windows 10 VM and allow it to set up a new Virtual Network and Subnet.
Next, i created a Linux (Ubuntu) VM using the same Resource Group and the same Virtual Network/Subnet.
i Used a username and password for Linux authentication so both VMs can connect on the same network.
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

Next, I configured a firewall (this will help me get a good intuition of what’s happening in the background). First, I’ll initiate a nonstop ping from the Linux VM to the Ubuntu VM by typing "ping 10.0.0.5 -t" in PowerShell, and this will keep pinging continuously.

![image](https://github.com/user-attachments/assets/812eacbc-b3f9-40d4-82bc-5f522019e730)

Next, I opened the network Firewall "Ubuntu VM" and disable incoming ICMP traffic. I will configure the Linux-VM cloud Firewall and tell it to block all incoming ping traffic. 

The Steps i took are:

 - Go to the Azure Portal

 - Search for “Virtual Machines”

 - Select your Linux VM from the list.

 - In the Linux-VM menu, scroll down and click “Networking.”

 - Under Network Settings, find “Network Security Group” and click on the link linux-vm-nsg. T(his is the firewall for your Linux VM).

 - In the NSG (Network Security Group) menu, click on “Inbound security rules.”

 - Click the “Add” button to create a new rule.

I set the Action to deny, set priority to 290 to put it above 300, and 290 will be evaluated first. 

   
![image](https://github.com/user-attachments/assets/1e7932ce-fd73-4773-b471-85215341f48d)

With the above rules set, ICMP traffic from any source will be denied. Once the rule takes effect, it will start timing out


![image](https://github.com/user-attachments/assets/0acb4245-1969-46d8-959e-9960f003bb23)

While observing Wireshark, I stopped seeing requests and replies, and all I could see were requests because no response was found; the Firewall blocked them out. If I go back and delete the "Deny" rule, it will start allowing the replies to happen again. Type Ctrl-C in powershell to stop the ping activity. 

![image](https://github.com/user-attachments/assets/f915ed7c-4f83-47e3-b976-84b8b668194e)

Here, i am obsering SSH traffic by getting the public IP address of the windows VM from Azure portal. SSH is used to make a secure connection from one computer to another. It uses TCP port 22. i went to windows computer and made an SSH connection into the linux computer and then observed the traffic. In powershell i typed "ssh labuser@ 10.0.0.5" which is linux-VM private IP address. 
       Whatever i typed traffic was sent to linux-VM through a secure channel. I am in windows-VM but i am connected to linux-VM through SSH. All the traffic in SSH is actually encrypted.

<p>
</p>

<p>

<p>
  
![image](https://github.com/user-attachments/assets/ad9de5f0-ac1b-4ae5-b06f-d6146a65ea2a)

At this point, i was observing DHCP traffic by creating a .bat file and i ran ".\dhcp.bat" in powershell. DHCP uses UDP port 67 and 68. This protocol is used to assign IP address to devices when they are first connected to the network. By typing "ipconfig/renew" in powershell, this command will drop the IP address that the computer has and will automatically broadcast for a new IP address. 
    Basically, what happened in the above picture is that when release occoured, the packet was sent from the source computer (windows-VM) to the destination computer which is the DHCP server in Azure. The 255.255.255.255 means broadcast. 
  
![image](https://github.com/user-attachments/assets/d0327954-eb86-4276-9875-d188712285bd) 

The above picture illustrates the client requesting an IP address, receiving an offer, acknowledging it, and eventually releasing the IP address.



![image](https://github.com/user-attachments/assets/a88b15ee-6154-4591-a2c9-1aae0ddf8fcf)

I also observed DNS traffic by typing "DNS" in powershell. Then i typed nslookup disney.com and the nslookup query retrieved an IP address from a DNS server that is not the primary source for the domain information.
     All DNS does is to resolve human readable names into IP addresses. 

![image](https://github.com/user-attachments/assets/f287784e-73d0-45ff-a257-27a34bf8eecd)

i copied the IP address, pasted it in the browser and i got the above image. i can see disney logo but it didn't open the website because i can't just load a website with an IP address.

![image](https://github.com/user-attachments/assets/c4a9b033-378a-4975-b8a6-a4877d5d9238)

To conclude this lab, I analyzed RDP traffic using a filter for TCP port 3389, which is the standard port used by the Remote Desktop Protocol. I observed a continuous stream of packets, which is expected, as RDP maintains a live session by constantly transmitting graphical interface data between the client and host systems. This allows users to remotely access and control another computer's desktop environment in real time.



</p>
<p>


</p>
<br />
