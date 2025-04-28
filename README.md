# Basic-Switch-Configuration

Objective:

● Simulate a console connection to a switch using Packet Tracer.

● Understand and configure basic switch settings.

● Learn to configure hostname, IP addresses, MOTD and passwords.

● Practice using show commands to verify switch configurations.

Software Requirements:

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

  5. Access the Switch via the Terminal on the PC
     
     ○ Click on the PC.
     
     ○ Go to the Desktop tab and click on the Terminal application.
     
     ○ Configure the terminal settings (leave the default settings: 9600 Baud rate, 8 data bits, no
parity, 1 stop bit).

     ○ You should now have access to the switch’s CLI (Command Line Interface).

Part 2: Verify the default switch configuration.

    In this step, you will examine the default switch settings, such as current switch configuration, IOS
    information, interface properties, VLAN information, and flash memory.
    
Switch> enable

  This command allows you to access Privileged EXEC Mode, where you can execute higher-level
commands. By default, the switch starts in User EXEC Mode with limited access.

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
   Switch#config t
to go our global exec mode and execute our commands

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

   
V. Configure a MOTD banner.

   Switch01(config)# banner motd #

Enter Text message. End with the character ‘#’.

Unauthorized access is strictly prohibited. #
