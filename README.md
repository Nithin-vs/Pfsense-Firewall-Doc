
# PfSense Firewall Setup and Configuration -Documentation

This project involves the installation and configuration of a pfSense firewall in a virtual machine environment, aimed at enhancing my understanding of network security and firewall management. The primary objective was to create a basic firewall setup that allows and blocks specific traffic, demonstrating the practical application of firewall rules. I successfully installed pfSense in a VM, configured its interfaces, and established connectivity between the pfSense firewall and a Windows virtual machine. Through this process, I learned about essential concepts such as inbound and outbound traffic control, the importance of documentation, and the hands-on experience of managing a firewall. Additionally, I explored various rule configurations, including blocking specific websites, which deepened my knowledge of how firewalls function to protect networks from unauthorized access. The project culminated in a comprehensive Word document detailing each step of the setup process, which serves as both a reference for future configurations and a demonstration of the skills acquired throughout this project. I intend to further expand my knowledge by exploring advanced features of pfSense, including VPN setups and intrusion detection systems (IDS).

## Authors

- [@Nithin-vs](https://github.com/Nithin-vs)


## Table of Contents

- Introduction

- What is Virtualization?

- What is PfSense?

- Downloading Vmware									

- Downloading PfSense									

- Making a new VM in Vmware								

- Configuring Interfaces									

- Accessing the web portal									

- Security											

- Basic Configuration										

- Setting up a firewall rule								

- Conclusion 



# Hi, I'm Nithin! 👋
As a Computer Science undergrad, I am driven by my passion for cybersecurity. Throughout my academic journey, I have learned programming languages and concepts of operating systems, software, hardware, and networks. One of my proudest accomplishments is obtaining an internship in Vulnerability Assessment and Penetration Testing. This experience allowed me to gain various aspects of knowledge in web penetration testing.
On this Documentation, I will be showing about the basic firewall setup and configuration using PfSense on the Vmware workstation.



## What is Virtualization?
Virtualization is a method of creating virtual versions of physical resources like servers or networks. It uses software to mimic hardware, allowing multiple operating systems and applications to run on one machine. This approach boosts efficiency and reduces costs. It started with mainframes, where it helped save expensive processing power by running several systems on one physical machine. There are various software which support the concept, for example Virtual box, Vmware etc. In simple terms, Virtualization helps make various operating system inside a host operating system. Running a Windows host and using virtualization running linux distros.
## What is PfSense?
PfSense is an open-source firewall and router software that runs on physical or virtual machines. It is used to secure and manage network traffic, offering features like firewall rules, VPNs, load balancing, and traffic monitoring. Designed for ease of use, PfSense can turn a regular computer into a powerful firewall, allowing you to customize and control network security. It's popular in both home and business environments for managing networks efficiently without expensive hardware.
## Downloading Vmware
Go to (https://www.vmware.com) and download the vmware workstation player for the preferred operating system. After downloading the .exe file, install it.

## Downloading PfSense
By going to the (https://www.pfSense.org/downloads) page we can get the PfSense latest stable version of ISO image which is provided by the Netgate. (Netgate is an open-source driven secure networking company that provides appliance and software-based firewall, VPN and routing solutions including PfSense.)
The website wants you to fill out the basic information about you and deliver the iso link on your email. After getting the email you can download the compressed file to your machine.
Extracting the zip file gives you the PfSense ISO.

## Making a New VM on Vmware
- Open the Vmware software and click the “Create a new Virtual machine” option on the right side.

- On the “Install disk image file (ISO)” option, browse the extracted PfSense ISO file and click next.

- Give Virtual machine a name and browse the storage location for the PfSense VM.

- Give the Virtual machine a required size and select the “Store virtual disk as singe file”.

- On the next step the Vmware gives us the summary of the VM. We are not finished yet, on the panel click “Customize Hardware” option.

- On the screen we have the options to customize hardware, change the memory to 2gb. We need at least two network adapters for setting up a firewall on pfSense, on the first attempt you don’t see two network adapters, for this you should click on the add option below to add a new network adapter
 
- The first network adapter should be set to bridged (Automatic) which acts as WAN to PfSense and the next network adapter should be kept on custom: Specific virtual network and set to the VMnet10.

- Then we are ready to fire the VM. On starting the PfSense installer..
## Configuring Interfaces 
- By selecting the option “Install pfSense”, need to configure the WAN and LAN interfaces to the pfSense this is crucial.

- On the next screen there are two adapters eM0 and eM1 with MAC addresses respectively. Let’s take a glance at the vm settings and locate to the bridged network adapter’s advanced tab. We see the MAC address of the adapter, same can be checked for the second adapter which is VMnet0. According to eM0 the bridged adapter is assigned and the eM1 is the VMnet0 adapter we configured when creating the VM. The eM0 should be assigned as WAN interface.

- After configuring the eM0 which has MAC address of “00:0C:29:DD:47:FE”, the WAN interface is assigned to the eM0 which is the bridged adapter in the VM settings.

- Then in the next step the installer ask us to configure the LAN interface for this the next adapter should be assigned. The eM1 in the installer signifies the VMnet10 in the VM settings of the next network adapter and LAN interface is configured to this eM1 interface which has a MAC address of “00:0C:29:DD:47:08”. This is configured to be our LAN interface for pfSense.

- After configuring we can proceed with the installation by checking the option “Proceed with the Installation”. Then the pfSense will try to reach its backend server and proceed us with the next step of “Install CE”. By checking the option the installation of pfSense starts. On installation completion the VM restarts and gives us the LAN IP of pfSense that can be entered in a web browser and we can access the web portal for pfSense.

- For obtaining the web portal, we cannot put the IP in the browser which is on the host. We should create a windows or a Linux distro with the network adapter setting configured to be set as VMnet10.

- We need to run the pfSense and the Windows VM at a stretch to make this possible.
## NOTE
Running more than one VM on a host machine simultaneously can drain out memory and processor from the host machine which in terms slows down the host machine and can cause errors.
## Accessing the web portal
- After complete installation the console shows us the WAN and LAN interface IP. The default IP address for the pfSense web portal is shown as 192.168.1.1/24.

- For accessing the web portal create a new windows VM and set the network adapter of windows machine to VMnet0 which is our pfSense eM1 which is LAN.

- After changing the network settings on the windows VM we are ready to fire up the VM. On the browser of the windows VM type the default LAN IP which we found on the pfSense (192.168.1.1).

- The default username and password is “admin” and “pfsense” respectively.
## Security
I recommend to change the default login credentials and the default LAN IP which gives us more security by not logging in the unauthorized people.
After changing the default password, set a TCP port number for the webConfigurator to override the default 80 for HTTP, 443 for HTTPS.

-  Go to System>Advanced>TCP port to set a new port number.

- Now without typing the full IP address without the port number in the browser, will not see the web portal.

- For security measures the LAN IP should be changed for the pfSense and new DHCP range should be configured.

- By going to Interfaces>LAN>IPV4 address, set a new IP address. In my case it is 192.168.20.1. After setting the address click on save and scroll top, there will be a option to apply changes click there. After clicking there your Windows VM will not receive internet. This is because the new IP you changed affects the DHCP range of IP. By forcing the windows network settings to use the new changed IP will bring back the the web portal.

- Go to control panel>Network and sharing centre>your adapter>properties>Internet protocol version 4(TCP/IPv4)>Use the following IP address and enter the changed LAN IP and just tap on the Subnet to auto set it.

- Now entering the new changed IP on the browser will give the web portal.

- After login go to Services>DHCP server and change the DHCP range. This change will allow the pfsense to automatically give IP address to the connecting client from the DHCP pool range which you will provide.

- After setting the DHCP you can change the network setting on the Network sharing center which in terms makes the pfsense to give IP from its DHCP pool to its client. Once again going to control panel>Network and sharing centre>your adapter>properties>Internet protocol version 4(TCP/IPv4) and set to the defaults “Obtain the IP address automatically"

- Now we can see the details of the IP which is allocated from the available pool of address from pfsense DHCP server.
## Basic Configuration
By changing the default LAN IP and configuring the new DHCP range of IP and by checking the pfsense firewall is alive or not by pinging the pfsense using its IP on the Windows VM confirms that the pfsense is automatically assigning the IP to the windows VM and the Windows VM is accessing the internet.
 
- The default LAN firewall rules are shown in the pfsense Web interface, going to Firewall>Rules>LAN.

- My basic Configuration of the pfsense firewall is configured and the windows VM is receiving the internet. But this basic rule allows all the network traffic to the LAN. 

- Now as a beginner I want to block some basic website that the windows VM should not access.

## Setting up a new firewall Rule
Let’s block a website which is https://www.example.com.

- In command prompt of the windows VM type the command 
nslookup www.example.com to view the website IP address. In my case there is a output of both IPv4 and IPv6 address.

- Now the both IP address should be added to the LAN rules as separate rules.

- Copy the IPv6 address and go to the web portal, go to Firewall>Rules>LAN and add (up arrow) option. Adding the rule as mentioned below.

- Copy the IPv4 address and go to the web portal, go to Firewall>Rules>LAN and add (up arrow) option. Adding the rule as mentioned below.

- By this configuration, clearing all the browsing data and cache, searching for the website https://www.example.com, the firewall now blocks the website and it is inaccessible.
## Conclusion
In this project, I explored the process of setting up a pfSense firewall within a virtual machine (VM) environment, which significantly enhanced my understanding of both firewall technology and virtualization.
### Key Learnings:
- Understanding firewall
- Hands-on experience with pfsense
- Virtualization skills
- Importance of documentation 
Overall, this project has been an invaluable learning experience, enhancing my technical abilities and preparing me for future endeavors in network security and administration.
