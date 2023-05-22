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

<h3>Setting up Virtual Machines</h3>

<p>
<img src="https://i.imgur.com/iLTteAK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Y3XeyoQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/SeDNxsg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the front page of the Microsoft Azure Portal, go into the search bar and search for "Virtual Machine". Click on that, and from there you'll see the option to create a new Azure Virtual Machine. To simplify things we'll have this VM named "VM1". We'll have the VM run Windows 10 Pro, using 2 Vcpus and 16GB memory. Once you create the username and password, swap over to the network tab and confirm that it is creating a new virtual network, as well as a new resource group. Once everything is validated you can press "Create"
  
</p>
<br />

<p>
<img src="https://i.imgur.com/RKCDVln.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we'll go ahead and create the 2nd VM. This time make sure the resource group is same as the newly-created VM1_group. Also keep in mind that the region must be the same as VM1's, otherwise the two machines will not be able to transmit to one-another. For VM2, instead of Windows 10 Pro we'll be using Ubuntu, with the same Vcpu and memory as VM1. Change the authentication type from "SSH public key" to "password" and fill it out, preferably with the same username and password as VM1. Once you've confirmed that the resource group, virtual network, and region are all the same as VM1's, you can now review + create VM2.
  
After VM2 is created, go to the start menu on your computer and type in "Remote Desktop Connection". Back in Azure, navigate to VM 1 and copy to clipboard the VM's Public IP Address, and paste that address into the Remote Desktop Connection. You will then be asked to enter the VM's credentials so fill in the VM's Username and Password that you had set up previously. After confirming you should have successfully entered VM1
</p>
<br />

<h3>Installing Wireshark</h3>

<p>
<img src="https://i.imgur.com/8Nx9ucw.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ebLwcex.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once we are in the VM, we will now download and install the program "Wireshark" to analyze data traffic moving from this VM to the internet and to VM2. Access the Microsoft Edge browser and search for "Wireshark Download" in the search bar. Locate the wireshark website and once inside, download the latest stable release of the program, and do a standard installation of the program on the VM. Once installation is complete, go to Start and type in "Wireshark" and start the program.
</p>
<br />

<p>
<img src="https://i.imgur.com/qmQJviA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Starting up Wireshark should bring up the image above. Click on "Ethernet and at the upper left of the program there is a blue button that says "start capturing packets". Click on that to begin analyzing traffic moving through the VM. Once you start capturing packets, click on the search bar that says "apply a display filter" right below the start button and type in "icmp" so it only shows traffic thats being moved from one IP to another. Before we can see traffic on icmp, we need to open up the command prompt, so go to the Start menu and type in "command prompt" or "cmd", and open up the 
</p>
<br />

<h3>Observing ICMP Traffic</h3>

<p>
<img src="https://i.imgur.com/Eux3MYF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/wAKrcmb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
With the command prompt now open we can begin observing icmp traffic. The first thing we'll ping is the Ubuntu Server on VM2. To do this we'll need to minimize VM1, go back to Microsoft Azure and head to VM2. Look for VM2's Private IP Address under the Networking category as shown in the 2nd image above, highlight the Private IP Address, and copy it onto your clipboard. Once we've done that, return back to VM1 and in the command prompt, we'll want to type in "ping (IP Address)". For this example we'll use 10.0.0.5 because that is the Private IP for VM2.
<p>
</p>
<br />

<p>
<img src="https://i.imgur.com/ZVWFn7s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After typing in "ping 10.0.0.5" in the command prompt, we see that small amounts of data were sent from VM1 to VM2, confirming that there is a working connection between the two VMs. Wireshark also confirms this by showing that packets were sent from VM1 (10.0.0.4) to VM2 (10.0.0.5) with a request, and has received a reply on all four packets. Knowing that there is a constant connection between the VMs with no errors reported, we can try sending a ping to a random website on the internet.
</p>
<br />

<p>
<img src="https://i.imgur.com/kpUhjo8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This time, we will try pinging Google to see if there is a connection. To do this, within the command prompt type in "ping www.google.com". What we see is that just like between the two VMs, there is both a ping request sent out from VM1 and a ping reply coming in from Google's Public IP Address.
</p>
<br />

<h4>ICMP Security Rule</h4>

<p>
<img src="https://i.imgur.com/9h90sfm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/YQMH5l0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/utfG1YE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
So now that we know that a ping helps determine a connection between 2 addresses, what happens when a server disables inbound traffic? To do this between our 2 VMs, first we will go to our command prompt in VM1 and type in "ping 10.0.0.5 -t". What this command does is send a perpetual ping to VM2. While this ping is occuring, minimize VM1 and return to the Microsoft Azure Portal. In the Search bar type in "Network Security Groups" and search for VM2. CLick on the VM2-nsg and look for "Inbound Security Rules", and click on "add" to add a new rule. For this new rule, we will be denying any traffic inbound to VM2 from any ICMP protocol. The priority number, which can be between 100 and 4096, dictates which rules precede what. So the lower the number in priority, the higher it is prioritized against other rules.
</p>
<br />

<p>
<img src="https://i.imgur.com/e1vHU9s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Going back into VM1, we can see that the new security is working and VM1's pings to VM2 are unable to find a response. When the system is unable to find a reply, it will be labeled as "request timed out". Now knowing how security rules work, we can first stop the perpetual ping by clicking on the command prompt and pressing ctrl+c to stop the ping. Next we'll go ahead and re-enable icmp pings to VM2.
</p>
<br />

<h3>Observing SSH Traffic</h3>

<p>
<img src="https://i.imgur.com/A3N0ogw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From VM1's Wireshark, return to the search bar and replace "icmp" with "ssh" to observe only SSH traffic. With SSH we can login remotely from VM1 to VM2 through the Command Prompt. To do this, we will type in "ssh (username)@(private IP)", fill in the blanks with the 2nd VM's username and Private IP. The command prompt will then give you a confirmation that you want to remote access VM2. Upon saying yes the command prompt will then ask for VM2's password. When typing it in, you'll notice that the password doesn't actually show up in the command line. This is intentional in order to avoid showing the password. Once you type out the correct password and press Enter, the command prompt will give you the information on the accessed device, like the image above. You now have a direct access to VM2 from VM1.
  
You'll notice that the Wireshark traffic shows that VM1 was attempting to access VM2 and once the appropriate information was sent in the Command line, a secured line has been created so now the two VMS can relay information to one-another. Once you're finished, to exit from VM2 in the command prompt, type "Exit" and press enter to return to VM1's command prompt.
</p>
<br />

<h3>Observing DHCP Traffic</h3>

<p>
<img src="https://i.imgur.com/rHbM4Or.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back in the Wireshark program, go to search display filter and replace "ssh" with "dhcp". DHCP is what assigns new IP addresses to networks. To see how this works, we go back to our Command Prompt and type in "ipconfig /renew". Because we are using a VM and releasing an IP address, which in turn disrupts the Remote Desktop Access to the VM, it will likely come out as an error but the traffic will show that the VM sent out request for a new IP, and was ultimately denied.
</p>
<br />

<h3>Observing DNS Traffic</h3>

<p>
<img src="https://i.imgur.com/U4CqtoN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Going back to Wireshark in the Display Filter search bar, change DHCP to DNS. Domain Name System (DNS) is what hostnames or websites use to connect themselves to an IP address. In the command prompt type in "nslookup www.google.com" or "nslookup www.youtube.com", and we see that these IP addresses go by an alias, which is the name of the sites.
</p>
<br />

<h3>Observing RDP Traffic</h3>

<p>
<img src="https://i.imgur.com/RbfX9My.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The final type of traffic we'll be looking at is the Remote Desktop Protocol (RDP). To only look at RPD traffic in Wireshark, go to the display filter and type in "tcp.port == 3389". You will immediately notice that traffic is currently moving through the VM on Wireshark. This is because data is constantly being transmitted from the Azure Server and the VM, even when nothing is going on in the VM at the surface. In a way you are watching a live-stream of VM1 and that data needs to be transmitted for you to see it, so there will always be a constant flow of traffic. 
</p>
<br />

