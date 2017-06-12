---
ID: 3331
post_title: Basic troubleshooting guide
author: frinxadmin
post_date: 2016-12-16 11:57:06
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/sbe-basic-troubleshooting-guide.html
published: true
sidebar:
  - ""
footer:
  - ""
header_title_bar:
  - ""
header_transparency:
  - ""
apost_date:
  - 'a:1:{i:0;s:19:"2016-11-16 12:51:40";}'
hheader_title_bar:
  - 'a:1:{i:0;s:17:"a:1:{i:0;s:0:"";}";}'
---
[wpmem_form login]

You can use this guide to help you identify and resolve basic problems you may experience with your SBE instance.

Each SBE container has the following pre-installed tools:

    netcat  
    ssh-client  
    ssh-server  
    telnet  
    

**SSH login credentials for each container:**

username: admin  
password: admin

Example of SSH login into "apache-ds" component container:

    docker exec -it sbe-default-gerrit service ssh start
    ssh admin@<compomonet-ip>
    

[/wpmem_form]