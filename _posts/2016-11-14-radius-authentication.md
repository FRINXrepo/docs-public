---
ID: 2553
post_title: RADIUS authentication
author: frinxadmin
post_date: 2016-11-14 07:34:16
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/radius-authentication.html
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
RADIUS is a network protocol which authenticates a user who connects and uses a network service. The user sends a request to a Network Access Server (NAS) to gain access to a particular network resource using access credentials. The NAS sends a RADIUS **AccessRequest** message to the RADIUS server, in our case freeRADIUS. The RADIUS server then checks that the information is correct using authentication schemes; in the case of the FRINX distribution, PAP is used. It can check the user information against an external resource such as LDAP in order to verify the user's information.

The response from the Radius server can be either: Access Accept - The user is granted access. This information may be stored locally on the RADIUS server, or may be looked up in an external source such as LDAP. Access Reject - The user is unconditionally denied access to all requested network resources. Reasons may include failure to provide proof of identification or an unknown or inactive user account.

### Quick Start

Within the FRINX distribution, the AAA feature extends authentication capabilities via the RADIUS protocol. In order to be able to authenticate the user it is necessary to start freeRADIUS, which acts as a RADIUS server.

**To download the freeRADIUS image:**

    docker pull docker.io/unico/freeradius
    

To run the freeRADIUS server:

    docker run -it docker.io/unico/freeradius
    

**Radius configuration**  
Within your FRINX distribution directory structure, go to the /etc directory and edit the *shiro.ini* file. Under "[main]" enter the following four lines of text:

radiusRealm = org.opendaylight.aaa.shiro.realm.RadiusRealm  
securityManager.realms = $radiusRealm  
radiusRealm.serverIp = 172.17.0.2  
radiusRealm.sharedSecret = dGVzdGluZzEyMw==

The final two lines set the RADIUS server ip address and shared secret string. The shared secret string is Base64 encoded.

**Prepare the environment**

Start the controller Karaf container:

    bin/karaf frinx.createtoken <user token>
    

Check the installed bundle for RADIUS authentication. It must be in ACTIVE state:

    la | grep -i aaa-authn-radius
    

Open the browser and type the following link: http://localhost:8181/index.html#/login Enter the credentials: username: admin password: password

If the credentials are correct, the RADIUS server sends \*AccessAccept\* and the user can access protected resources.

**Change RADIUS credentials**

Start the freeRADIUS docker image:

    docker exec -it &lt;CONTAINER_ID&gt; /bin/bash  
    

Go to /etc/freeradius and open the users file:

    vi /etc/freeradius/users  
    

Check the line where the default user is defined e.g.:

admin Cleartext-Password := "password"

Change the username and password and save the file. Next, exit from the container and restart the docker image:

    docker stop <CONTAINER_ID>   
    docker start <CONTAINER_ID>
    

[/wpmem_form]