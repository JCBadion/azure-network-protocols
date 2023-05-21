# Azure-Network-Protocols
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Set up Virtual Machines (VM) using Microsoft Azure, one for Windows 10 and one for the Ubuntu server
- Remote Access into the VM
- Download and Install Wireshark
- Observe traffic between the two Virtual Machines
- Observe traffic from the Virtual Machine and the Web.

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/iLTteAK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Y3XeyoQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/SeDNxsg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the front page of the Microsoft Azure Portal, go into the search bar and search for "Virtual Machine". Click on that, and from there you'll see the option to create a new Azure Virtual Machine. To simplify things we'll have this VM named "VM1". We'll have the VM run Windows 10 Pro, using 2 Vcpus and 16GB memory. Once you create the username and password, swap over to the network tab and confirm that it is creating a new virtual network, as well as a new resource group. Once everything is validated you can press "Create"
  
After VM2 is created, go to the start menu on your computer and type in "Remote Desktop Connection". Back in Azure, navigate to VM 1 and copy to clipboard the VM's Public IP Address, and paste that address into the Remote Desktop Connection. You will then be asked to enter the VM's credentials so fill in the VM's Username and Password that you had set up previously. After confirming you should have successfully entered VM1
</p>
<br />

<p>
<img src="https://i.imgur.com/RKCDVln.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we'll go ahead and create the 2nd VM. This time make sure the resource group is same as the newly-created VM1_group. Also keep in mind that the region must be the same as VM1's, otherwise the two machines will not be able to transmit to one-another. For VM2, instead of Windows 10 Pro we'll be using Ubuntu, with the same Vcpu and memory as VM1. Change the authentication type from "SSH public key" to "password" and fill it out, preferably with the same username and password as VM1. Once you've confirmed that the resource group, virtual network, and region are all the same as VM1's, you can now review + create VM2.
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
