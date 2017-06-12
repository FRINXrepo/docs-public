---
ID: 4583
post_title: Installation
author: frinxadmin
post_date: 2017-05-29 14:38:33
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-vpp-distribution/vpp-operations-manual/installation-tips.html
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

### VPP Installation

Described at: [VPP install packages][1]

If VPP does not pick up interfaces, it helps to build and install it manually:

    ./build-root/vagrant/build.sh
    cd build-root
    sudo dpkg -i *.deb
    sudo service vpp start
    

**The following resources are useful in figuring out how to do (configure) something with VPP**

1.  <https://wiki.fd.io/view/VPP>
2.  [https://docs.fd.io/vpp/17.04/][2]
3.  Google 
4.  **CSIT (VPP integration tests) - they use VAT tool to provide complex configuration to VPP. Each test case logs exact configuration steps. So looking at log file from latest vpp functional test run can help <https://jenkins.fd.io/view/csit/job/csit-vpp-functional-master-ubuntu1604-virl/> If log file does not open directly, download and reopen in browser). Look at a test case, list of keywords and vat command executed in every step.** 
5.  vpp-dev@lists.fd.io

### Install VPP in a docker container

After docker is installed start a centos7 container:

    sudo docker run -ti --privileged centos7 /bin/bash
    

Then in the container install vpp, configure and start it:

     yum install install apt-transport-https vim net-tools inetutils-ping telnet
    
        cat <<EOT >> /etc/yum.repos.d/fdio-release.repo
        [fdio-release]
        name=fd.io release branch latest merge
        baseurl=https://nexus.fd.io/content/repositories/fd.io.centos7/
        enabled=1
        gpgcheck=0
        EOT
    
        yum install vpp
    
    
    # More info on VPP install: https://wiki.fd.io/view/VPP/Installing_VPP_binaries_from_packages
    
    vim /etc/vpp/startup.conf
    # Change DPDK configuration to add "no-pci" config attribute
    # dpdk {
    #    uio-driver uio_pci_generic
    #    no-pci
    # }
    
    # And enable cli
    # unix {
    # nodaemon
    #  log /tmp/vpp.log
    #  full-coredump
    #  cli-listen localhost:5002
    # }
    
    /usr/bin/vpp -c /etc/vpp/startup.conf &
    telnet 0 5002
    

To save the modified container invoke from host:

    sudo docker commit a4fdd4da4500 temp/vppcentos
    

### Installing binary packages

Instructions for consuming publicly available binary packages of FD.FRINX.io distribution

**Centos7**

In file:

    /etc/yum.repos.d/frinx-fdio-release.repo
    

Set content:

    [frinx-fdio-release]
    name=FRINX fd.io release branch latest merge
    baseurl=https://<CustomerID>:<CustomerPassword>@nexus.fd.frinx.io/nexus/content/repositories/fd.io.centos7/
    enabled=1
    gpgcheck=0
    sslverify=0
    

***Make sure to change the CustomerID and password in the repository settings***

Installation with YUM can be done with:

    sudo yum install vpp vpp-plugins vpp-monitoring-agent
    

[/wpmem_form]

 [1]: https://wiki.fd.io/view/VPP/Installing_VPP_binaries_from_packages
 [2]: https://wiki.fd.io/view/VPP