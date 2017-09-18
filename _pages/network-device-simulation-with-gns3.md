---
ID: 5762
post_title: Network device simulation with GNS3
author: frinxadmin
post_excerpt: ""
layout: page
permalink: >
  https://frinx.io/network-device-simulation-with-gns3
published: true
post_date: 2017-09-13 08:43:13
---
**Network device simulation with GNS3**

This guide shows how to setup and run GNS3 simulation with IOS devices.  
It also makes the devices available in an internal network for possible ODL testing.  
All running locally with just approx. 4 GB of RAM.

> This guide is aimed at WINDOWS + VIRTUAL BOX. Virtualbox does not support nested virtualisation so there might be warnings from GNS3 that the devices will be slow. However for basic configuration it is sufficient.

### SETUP

Prerequisites:

Virtualbox installed

### Installing GNS

[Background][1]

[Download GNS3VM][2]

Import the VM into Virtualbox  
Set the RAM to 4GB and CPU to 2 cores  
There should be 2 network ports preconfigured, add a 3rd one (Host only connection)  
Start the VM  
Just check whether it starts  
Stop the VM

[Download the GNS3 APP][3]

Install it + **ALL THE SUGGESTED TOOLS**  
If asked, pick the option for using GNS3 VM  
Start the APP and point to your VM

IOS images can be downloaded from Cisco and many other sources on the Internet.

In the GNS3APP import IOS router **FOR GNS 3 VM**: <https://protechgurus.com/how-to-add-router-ios-image-in-gns3/>

### Running simulated devices

### Starting IOS device

Drag and Drop the IOS device in the app  
Right click and start  
Right click and open CLI to check if its all ok

### Connecting to Virtualbox network

The desired network setup:

![alt text][4]

Go into the GNS3VM's shell  
Create a bridge: `sudo ip link add name fw type bridge`  
Start the bridge: `sudo ip link set fw up`  
Create a tap interface for each IOS: `sudo tunctl`  
Turn the tap interface on: `sudo ip link set tap0 up`  
Add the tap interface to bridge: `sudo ip link set tap0 master fw`  
Turn on VM's host only network NIC: `sudo ifconfig eth2 up`  
Flush IP address from VM's host only network NIC: `sudo ip add flush eth`  
Add that NIC into bridge: `sudo ip link set eth2 master fw`

### Connecting IOS device to tap interface

In GNS3 drop a cloud into the simulation

*   The cloud needs to represent GNS3 VM
*   In the configuration of the cloud add all the tap interfaces

Drag a link between the cloud and IOS device

*   Cloud end needs to be anchored to the tap interface
*   IOS end needs to be anchored to one of IOS interfaces

The result should look like this:

<img src="https://frinx.io/wp-content/uploads/2017/09/t.png" alt="" width="1664" height="964" class="alignleft size-full wp-image-5772" />

GNS3 project file can be accessed [here][5]

POSTMAN can be accessed [here][5]

**Configure IOS interface**

Open IOS shell from GNS  
Configure ( This is assuming host-only network is 192168.56.0/24 ):

    enable
    conf t
    interface FastEthernet0/0
    no shutdown
    ip address 192.168.56.121 255.255.255.0
    exit
    exit
    

Now you should be able to ping your DEV VM from within IOS:

    ping 192.168.56
    

## Mounting simulated IOS with ODL in DEV VM

Now you can proceed with mounting both of the devices in ODL, using CLI's [POSTMAN collection][5]. But before that, both devices need to enable remote management.

**Configure Telnet on IOS**

    enable
    conf t
    enable password cisco
    interface FastEthernet0/0
    ip address 192.168.56.122 255.255.255.0
    no shutdown
    exit
    exit
    
    conf t
    line vty 0 4
    password cisco
    login
    exec-timeout 40
    motd-banner
    exit
    exit
    

**Configure SSH on IOS**

    enable
    
    conf t
    enable password cisco
    interface FastEthernet0/0
    ip address 192.168.56.121 255.255.255.0
    no shutdown
    exit
    exit
    
    configure terminal
    hostname R121
    ip domain-name FRINX.LOCAL
    crypto key generate rsa
     1024
    ip ssh version 2
    line vty 0 4
     transport input ssh
     login local
     exit
    username cisco password cisco
    exit
    

## Running an IOS XR image on GNS

Chose an IOS XR ova image from [here][6]

[convert it to qcow2 format][7].

import the IOS XR image as a Qemu VM in GNS3.

<img src="https://frinx.io/wp-content/uploads/2017/09/Screen-Shot-2017-07-05-at-1.29.46-PM.png" alt="" width="1566" height="1342" class="alignleft size-full wp-image-5773" />

Add more NICs

<img src="https://frinx.io/wp-content/uploads/2017/09/Screen-Shot-2017-07-05-at-1.27.24-PM.png" alt="" width="2104" height="1410" class="alignleft size-full wp-image-5774" />

 [1]: https://www.gns3.com/support/docs/quick-start-guide-for-windows-us
 [2]: https://www.gns3.com/software/download-vm
 [3]: https://www.gns3.com/software/download
 [4]: https://frinx.io/wp-content/uploads/2017/09/gns3nwrt.png
 [5]: https://github.com/FRINXio/GNS3
 [6]: https://frinx.sharepoint.com/Frinx%20team/Shared%20Documents/DEVELOPERS/IOS_image
 [7]: http://ask.xmodulo.com/convert-ova-to-qcow2-linux.html