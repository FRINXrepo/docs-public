---
ID: 2691
post_title: Developer Guide (old)
author: ngray@frinx.io
post_date: 2016-11-16 12:51:40
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/sbe-developer-guide.html
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
**Download and install JDK 8**  
Fedora

    sudo dnf install java-1.8.0-openjdk java-1.8.0-openjdk-devel
    

Ubuntu

    sudo apt-get install openjdk-8-jdk
    

**Download and install Maven**

Fedora

    sudo dnf install maven
    

Ubuntu

    sudo apt-get install maven
    

**Optional: Install Wireshark**

Wireshark is a packet capture and inspection tool. It can be useful when working with southbound plugins. To install Wireshark run the following commands in a terminal.

Fedora

    sudo dnf install wireshark
    

Ubuntu

    sudo apt-get install wireshark
    

**Optional: Increase the amount of RAM maven can use** You can tell allocate more memory to maven by setting the MAVEN_OPTS environment variable. To do this, edit your ~/.bashrc (or ~/.zshrc, or similar depending on you shell):

    vim ~/.bashrc
    

Add the following:

     export MAVEN_OPTS='-Xmx1048m -XX:MaxPermSize=512m
    

Note, you can increase the heap space, the -Xmx setting, to greater than 1G if memory is available.

When building in maven, the max memory reached will be displayed at the end of the build. You can use this as a guide to determine if more memory would help decrease build times. Approximately 1.5G of RAM is needed by the JVM to run the Helium Controller repeatedly and avoid OOM errors.

## 2\. Repository relationship

**Figure 1: Repository relationship** ![Figure 1: Repository relationship][1]

## 3\. Building ODL project locally

OpenDaylight maintains its own repositories outside of Maven Central, which means that maven cannot resolve OpenDaylight artifacts by default. Since OpenDaylight is organized as multiple inter-dependent projects, building a particular project usually means pulling in some artifacts. In order to make this work, your maven installation needs to know the location of OpenDaylight repositories and has to taught to use them.

This is achieved by editing your local settings.xml file (the default path for the file is ~/.m2/settings.xml).

 [1]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc/master/figures!repository_schema.png "Figure 1: Repository relationship"