---
ID: 2681
post_title: Installation
author: ngray@frinx.io
post_date: 2016-11-16 12:46:12
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/sbe-installation.html
published: true
sidebar:
  - ""
footer:
  - ""
header_title_bar:
  - ""
header_transparency:
  - ""
---
[wpmem_form login]

The FRINX SBE runs on one or multiple hosts. The following instructions explain how to install it on one host. For installations across multiple hosts please contact info@frinx.io.

*   Prepare the host
*   Install prerequisites
*   Get project sources
*   Pull Docker containers
*   Run container suite
*   Create LDAP users
*   Verify installation

## 1\. Prepare the host

Create a VM or a physical machine with the following specifications:

**Minimal host configuration**  
CPU 4 Cores  
8 GB RAM  
Disk space: 50 GB

**Recommended host configuration**  
CPU 8 Cores  
16 GB RAM  
Disk space: 100 GB

Note - if you are installing the SBE on a virtual machine, ensure its network adapter is set to 'bridged'. For example, in VirtualBox Manager this can be done by going to Settings>Network.

**We have tested the FRINX SBE on the following OS**  
Ubuntu 16.04.1 LTS server  
Fedora 24

## 2\. Install prerequisites

In the following steps we will take you through the installation of the prerequisites on the host that will run the FRINX SBE.

<table>
  <thead>
    <tr>
      <th>
        Prerequisite
      </th>
      
      <th>
        Recommended version
      </th>
      
      <th>
        Note
      </th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td>
        Docker
      </td>
      
      <td>
        1.10.x
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        Git
      </td>
      
      <td>
        2.7.x
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        OpenSSL
      </td>
      
      <td>
        1.0.2
      </td>
      
      <td>
      </td>
    </tr>
  </tbody>
</table>

You can install all prerequisites for the FRINX SBE with the following commands:

**Fedora**

    sudo dnf update
    sudo dnf install docker git-core
    

If you have problems installing Docker with the above command, you can find an alternative method of installation here: [Docker guide][1]

**Ubuntu**

    sudo apt-get update
    sudo apt-get install docker.io git-core
    

If you have problems installing Docker with the above command, you can find an alternative method of installation here: [Docker guide][2]

**Fedora and Ubuntu**

The next steps enable you to manage Docker as a non-root user, so that you no longer have to type "sudo" before every docker command. This only has to be done once  
**Note: after entering the following commands you need to log out and back in for them to take effect**.

    sudo groupadd docker
    sudo usermod -aG docker [username]
    

## 3\. Get project sources

In this step you clone the configuration files and operational scripts from our git repository onto your host.

If you are not sure where to install the repository, choose your home directory (cd ~) for the installation.

You can obtain a customername and customerpassword from your FRINX representative at <info@frinx.io> for a licensed and supported installation. Alternatively, use the demo credentials:

**[customername]: sbecustomer**

**[customerpassword]: please contact info@frinx.io**

The following command can be run from any directory on the VM host machine and will create a directory named ‘sbe’ in your current directory.

    git clone https://[customername]@gerrit.frinx.io/sbe
    cd sbe
    

When prompted for a password enter the [customerpassword] provided by FRINX.

### 3\.1 Update the project (Optional)

Whenever you want to update the local repository with a newer version of the content from FRINX, run the following command in the directory sbe/

    git checkout [version]
    git pull 
    

***where [version] is e.g. x4***

## 4\. Pull Docker images

Run the script that downloads all FRINX SBE Docker containers onto your host. The script is located in the directory sbe/

    ./sbe pull-images
    

This step can take tens of minutes depending on your download speeds.

## 5\. Run the container suite

Use the command below to run the container suite. The script (located in 'sbe') runs the containers in persistent mode and creates the Docker network.

    ./sbe start
    

This step can take a few minutes. If you receive an error message related to Docker please ensure you have run the commands at the end of step 2:

    sudo groupadd docker
    sudo usermod -aG docker [username]
    

**Note: after running the above commands you must log out and back in for them to take effect**

You can check if all containers are up with the following command:

    ./sbe ls
    

## 6\. Create LDAP users

### Import the LDIF file into the Apache Directory server

Issue the following command on your host to update the LDAP configuration in the Apache Directory server container. Go to directory ~/sbe/ and type:

    ./sbe run ldap-import base.ldif
    

### Add additional users

Now we add additional users to Apache Directory server: First [download Apache LDAP Studio][3]  
Note the following are required: xwindows  
linux GUI  
Java SRE

After installing Start Apache Directory Studio, start it and from the top menu, **click on LDAP > New connection:**

In the window that opens, set the parameters as follows:  
**Connection name** can be anything you choose.  
For **Hostname**, enter the IP address of NET_IP_APACHEDS in the sbe/instances/default/config file.  
**Port** is 10389  
On the second screen (Authentication), change the authentication method to "No authentication"  
Click on Finish.

**1\. In ApacheDS Studio, open the LDAP perspective**

**2\. In the menu on the left, navigate to: Root DSE -> dc=example,dc=com -> ou=accounts -> uid=admin** ![first][4]

**4\. Right-click on uid=admin and select New -> New Entry**  
![third][5]

**5\. In the dialog box, select "Use existing entry as template" click Next**  
![fourth][6]

**6\. Again click on next**  
![fifth][7]

**7\. Rename uid "admin" value to e.g: "johnny", then click on next** ![sixth][8]

**8\. Now you can customize user detail, eg. givenName, mail, displayName, uid, userPassword (double click on an item to access it)** ![new][9]  
**DO NOT FORGET TO CHANGE userPassword**

Repeat the process for any additional users you wish to add.

## 7\. Verify installation

**Edit your hosts file to add host names**

Edit your system hosts file:

For Windows, instructions can be found on the Microsoft website.  
For Mac/Linux:

Open the file for editing:

    sudo vi /etc/hosts  
    

OR

    sudo gedit /etc/hosts  
    

Add the following lines:

    10.0.0.1 [hostname]  
    10.0.0.1 jenkins.[hostname]  
    10.0.0.1 gerrit.[hostname]  
    10.0.0.1 nexus.[hostname]  
    10.0.0.1 redmine.[hostname] 
    10.0.0.1 sonarqube.[hostname] 
    

*Replace **10\.0.0.1** with the IP address of the physical or virtual machine where the SBE is provisioned.*  
*Replace **[hostname]** with the HOST_NAME entry in **sbe/instances/default/config**. For most users this will be **localhost**.*

**As an alternative to editing your hosts file, you can instead choose to enter these details as A entries in BIND format in your DNS server.** The following format should be used for these entries:

    jenkins    A   10.0.0.1  
    gerrit     A   10.0.0.1  
    nexus      A   10.0.0.1  
    redmine    A   10.0.0.1  
    sonarqube  A   10.0.0.1
    

Make sure each host in your environment is configured to resolve hostnames from your DNS server.

**Verify Installation**

In a Web browser, go to http://[hostname]/  
*Replace [hostname] with whatever you set in the **/etc/hosts** file (see above).*  
Now you can directly access the various FRINX SBE services:

**Figure 4: SBE Access Verification**

![Figure 4: SBE Access Verification][10]

*   Try to log in to each service by clicking on the **'View'** button. The usernames and passwords are:

<table>
  <thead>
    <tr>
      <th>
        Service
      </th>
      
      <th>
        Login credentials
      </th>
      
      <th>
        URL
      </th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td>
        Nginx
      </td>
      
      <td>
        N/A
      </td>
      
      <td>
        http://[hostname]/
      </td>
    </tr>
    
    <tr>
      <td>
        Gerrit
      </td>
      
      <td>
        Use the LDAP password you created in Step 6.
      </td>
      
      <td>
        http://gerrit.[hostname]/
      </td>
    </tr>
    
    <tr>
      <td>
        Nexus
      </td>
      
      <td>
        Use the LDAP password you created in Step 6.
      </td>
      
      <td>
        http://nexus.[hostname]/
      </td>
    </tr>
    
    <tr>
      <td>
        Jenkins
      </td>
      
      <td>
        Use the LDAP password you created in Step 6.
      </td>
      
      <td>
        http://jenkins.[hostname]/
      </td>
    </tr>
    
    <tr>
      <td>
        Redmine
      </td>
      
      <td>
        Use the LDAP password you created in Step 6.
      </td>
      
      <td>
        http://redmine.[hostname]/
      </td>
    </tr>
    
    <tr>
      <td>
        SonarQube
      </td>
      
      <td>
        N/A No login credentials are required
      </td>
      
      <td>
        http://sonarqube.[hostname]/
      </td>
    </tr>
  </tbody>
</table>

*   Each service can also be accessed directly via the URLs listed in the above table

**Optional - Setting up LDAP for Nexus**  
In order to enable LDAP authentication for Nexus, do the following (Note - these steps are not necessary to use Nexus. They are only required if you wish to force LDAP authentication for accessing Nexus):

*   Log in to Nexus as 'admin' user
*   Click on **'Server administration and configuration'**
*   Select the **'LDAP'** item in the menu on the left side
*   Click on **'Create LDAP connection'**
*   Add name of connection into field **'Name'**, e.g. 'MyLDAPConnection'
*   Select protocol **'ldap'**, add hostname **'apacheds'**
*   Enter port **10389**, or port defined in your instance configuration file
*   In the field **'LDAP location'** enter 'dc=example,dc=com'
*   Select **'Authentification Method'** -> 'Anonymous Authentification'
*   Click on **'Verify connection'**, should display: Connection to LDAP server verified: ldap://apacheds:10389
*   Click on the **'Next'** button
*   In the field **'Configuration template'** select 'Generic Ldap Server'
*   In the field **'BaseDN'**, enter -> 'ou=accounts'
*   Click on **'Create'**
*   *Now try to logout and log in to Nexus using LDAP credentials*

[/wpmem_form]

 [1]: https://docs.docker.com/engine/installation/linux/fedora/ "Docker guide"
 [2]: https://docs.docker.com/engine/installation/linux/ubuntulinux/ "Docker installation guide"
 [3]: http://directory.apache.org/studio/downloads.html
 [4]: https://frinx.io/wp-content/uploads/2016/11/1.png "first"
 [5]: https://frinx.io/wp-content/uploads/2016/11/2.png "second"
 [6]: https://frinx.io/wp-content/uploads/2016/11/3.png "third"
 [7]: https://frinx.io/wp-content/uploads/2016/11/4.png "fourth"
 [8]: https://frinx.io/wp-content/uploads/2016/11/5.png "fifth"
 [9]: https://frinx.io/wp-content/uploads/2016/11/6.png "new"
 [10]: https://frinx.io/wp-content/uploads/2016/11/nginx.png "Figure 4: SBE Access verification"