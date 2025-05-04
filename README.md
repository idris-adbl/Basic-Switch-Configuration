# Basic-Switch-Configuration


![Screenshot 2025-04-28 210200](https://github.com/user-attachments/assets/da51e79a-a820-401f-a2af-150d79dc884f)



**Objective:**

 ● Simulate a console connection to a switch using Packet Tracer.

 ● Understand and configure basic switch settings.

 ● Learn to configure hostname, IP addresses, MOTD and passwords.

 ● Practice using show commands to verify switch configurations.

**Software Requirements:**

   - CISCO Packet Tracer

Part 1: Simulating the Console Connection Using Packet Tracer

    1. Open Cisco Packet Tracer and Create a Topology
   
    ○ Launch Packet Tracer.

    ○ Add the following devices to your workspace:

     ■ One Cisco 2960 Switch.

     ■ One PC.

     ■ One Console Cable

  2. Connect the PC to the Switch Using a Console Cable
     
○ In Packet Tracer, select the Console Cable from the cable options.

○ Click on the PC and connect the cable to the RS-232 port (also known as the console
port).

○ Click on the Switch and connect the other end to the Console Port.

3. Access the Switch via the Terminal on the PC
     
○ Click on the PC.
     
○ Go to the Desktop tab and click on the Terminal application.
     
○ Configure the terminal settings (leave the default settings: 9600 Baud rate, 8 data bits, no
parity, 1 stop bit).

○ You should now have access to the switch’s CLI (Command Line Interface).

Part 2: Verify the default switch configuration.

In this step, you will examine the default switch settings, such as current switch configuration, IOS information, interface properties, VLAN information, and flash memory.
    
         Switch> enable

This command allows you to access Privileged EXEC Mode, where you can execute higher-level commands. By default, the switch starts in User EXEC Mode with limited access.

I. Examine the current running configuration file.

         Switch# show running-config

II. Examine the startup configuration file in NVRAM.

         Switch# show startup-config

III. Examine the Cisco IOS version information of the switch.

         Switch# show version
  
IV. Examine the default VLAN settings of the switch.

         Switch# show vlan
  
V. Examine flash memory.

         Switch# show flash

 **Configure Basic Network Device Settings** 
          
To go our global exec mode and execute our commands
          Switch#conf t
          
Configure basic switch settings including hostname, local passwords and MOTD banner.

I. Assign the switch hostname.

         Switch(config)# hostname Switch01
    
II. Configure password encryption.

         Switch01(config)# service password-encryption

III. Assign class as the secret password for privileged EXEC mode access.

         Switch01(config)# enable secret class
    
This sets an encrypted password for accessing Privileged EXEC Mode. Encrypting the password
adds a layer of security.

IV. Prevent unwanted DNS lookups.

         Switch01(config)# no ip domain-lookup

V. Configure a MOTD (Message Of The Day) banner.

         Switch01(config)# banner motd #

Enter Text message. End with the character ‘#’.

e.g Unauthorized access is strictly prohibited. #


VI. Console port access should also be restricted. The default configuration is to allow all console connections with no password needed. To prevent console messages from interrupting commands, use the logging synchronous option.

         Switch01(config)# line con 0

         Switch01(config-line)# password cisco

         Switch01(config-line)# login

         Switch01(config-line)# logging synchronous

         Switch01(config-line)# exit

         Switch01(config)#
         
**Configure an IP Address on VLAN 1**

         Switch01(config)# interface vlan 1

         Switch01(config-if)# ip address 192.168.1.5 255.255.255.0

         Switch01(config-if)# no shutdown

VLAN 1 is the default VLAN on most switches. Assigning an IP address to VLAN 1 allows you to
remotely manage the switch. The no shutdown command ensures the interface is activated

**Configure a Default Gateway**

         Switch(config)# ip default-gateway 192.168.1.1
         
The default gateway allows the switch to communicate with devices outside its local network,
enabling remote management from different subnets.

**Enable Remote Management SSH (more secure):**

**Enable SSH for remote access**

**Create a local user**

          Switch01(config)#username admin privilege 15 secret cisco

Level 15: Full Access to all commands such as " reload " command, and the ability to make configuration changes.

Level 1 : Read-Only and access to limited commands, such as the "ping" command.

Secret ensures that the password is encrypted when stored in the switch's configuration file.

Switch needs to generate RSA encryption keys for secure communication when using SSH

**Create a domain name**

           Switch01(config)#ip domain-name mydoamin.local

**Generate RSA keys for SSH**
           Switch01(config)#crypto key generate rsa
           
The name for the keys will be: Switch01.mydomain.local

Choose the size of the key modulus in the range of 360 to 2048 for your general Purpose Keys. Choosing a key modulus greater than 512 may take a few minutes.

How many bits in the modulus [512]: 1024

% Generating 1024 bit RSA keys, keys will be non-exportable...[OK]

**Enable SSH for remote access:**
          Switch01(config)#ip ssh version 2
          
          Switch01(config)#line vty 0 15
          
          Switch01(config-line)#transport input ssh
          
          Switch01(config-line)#login local
          
**Test Remote Access for SSH**

**Open the Command Prompt on the PC and type:**

          PC> ssh -l admin 192.168.1.5
          
**Enter the password to access the switch securely via SSH.**

Verification commands:

          Switch# show ip interface brief
          
          Switch# show run
