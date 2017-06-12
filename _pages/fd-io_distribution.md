---
ID: 4095
post_title: FRINX FD.io Distribution
author: frinxadmin
post_date: 2017-03-24 13:24:34
post_excerpt: ""
layout: page
permalink: https://frinx.io/fd-io_distribution
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
### Fast Data Plane - FD.io

FRINX offers customers an alternative to the existing Openstack networking options when they require a simple and feature rich networking solution with unmatched deterministic data plane throughput and rich analytics.

We provide a supported distribution of the FD.io technology, which brings enormous improvements in software-based packet-processing performance, drawing on Cisco development and several years of production deployment experience.

For questions and orders please contact our team at <a href="mailto:info@frinx.io" target="_blank">info@frinx.io</a>.

### FRINX FD.io VPP Distribution & ML2 Driver

Customers who run data plane hungry applications like media production and network function virtualization in Openstack, benefit from the FRINX FD.io/ML2 distribution by gaining feature rich, deterministic packet forwarding in user space together with a lightweight monitoring agent developed by FRINX. <img src="https://frinx.io/wp-content/uploads/2017/03/d3.png" alt="" width="1024" height="460" class="aligncenter size-full wp-image-4104" />

The components of the distribution are described below.

#### VPP (Vector Packet Processor)

The VPP platform is an extensible framework that provides out-of-the-box production quality switch/router functionality.​ ​

The design of VPP is hardware, kernel, and deployment (bare metal, VM, container) agnostic​.

*   *It runs completely in userspace​* 
*   *Runs on x86, ARM, and Power architectures* 
*   *It's fast​ - outperforms available solutions:* ​ [OVS-DPDK vs VPP performance comparison​][1] ​ ​ 
*   *Based on DPDK*​ ​ 
*   *Open source​ FD.io*​ Plugins/management agents/tools​ Extensible design 
*   *Proven​ Since 2002*

#### OpenStack ML2 (Modular Layer 2)

The OpenStack Neutron plug-in (introduced in Havana) ​is a framework allowing OpenStack Neutron to simultaneously utilize the variety of layer 2 networking technologies found in complex real-world data centers​. It deprecates existing plugins such as OVS or Linuxbridge.

​**Type Drivers**: define how an OpenStack network is technically realized.​

**Mechanism Drivers**: responsible for taking information supplied by Type Drivers and ensuring it is properly applied given the specific networking mechanisms which have been enabled.​

​**Support for vendor mechanism drivers**: ALE Omniswitch, Arista, Brocade, Cisco Nexus, DCFabric, Lenovo… ﻿Multiple mechanism and type drivers can be used simultaneously to access different ports of the same virtual network.

#### FRINX Analytics agent for VPP

The FRINX proprietary analytics agent brings monitoring and an analytical aspect to VPP​. It allows the extraction of network data statistics and log information from the data plane to make it available via a Kafka stream or store it as simple log files. ​

<img src="https://frinx.io/wp-content/uploads/2017/03/magent.png" alt="" width="861" height="501" class="alignleft size-full wp-image-4364" />

<br clear="all" />

*It is:*

*   Very lightweight:​ 
*   Built with Golang + Cgo​ 

​*It collects:*​

*   Interface state change​ 
*   Interface info​ 
*   Bridge domain info​ 
*   Interface traffic stats​ 
*   Global traffic stats​

​*It produces:*​

*   Log​ 
*   Kafka

#### VPP Management

A range of management agents can be used as per customer requirements. In its basic form, VPP provides very low-level shared memory APIs that can be accessed from C code. Because this offers limited functionality, higher level APIs have been developed. For example, Honeycomb was developed on top of those binary APIs to provide Java APIs, on top of which NETCONF and RESTCONF were developed by borrowing from OpenDaylight. Essentially, Honeycomb exists as a management extension for VPP.

<img src="https://frinx.io/wp-content/uploads/2017/03/d2.png" alt="" width="338" height="210" class="alignleft size-full wp-image-4105" />

<br clear="all" />

Local: Low-level interfaces​  
*(primary) shared-memory binary APIs* ​  
*(debug) CLI*​  
*(testing) VPP-API-TEST tool*​ ​

Local: High level interfaces​  
*Java​*  
*Python*​  
*Lua*​ ​

Remote: Management agent​  
*Honeycomb​*  
*ML2 Python driver*​

#### VPP Use Cases

*vSwitch/vRouter*  
VMs Linux Namespaces/Containers

*VNF​*  
router, firewall, load-balancer

[Openstack ML2 driver with VPP][2]​

[OPNFV’s FastDataStacks project][3]​

Please reach out to us at [info@frinx.io][4] to schedule a trial or for further information.

 [1]: http://www.lightreading.com/nfv/nfv-tests-and-trials/validating-ciscos-nfv-infrastructure-pt-1/d/d-id/718684?page_number=8
 [2]: https://github.com/openstack/networking-vpp
 [3]: https://wiki.opnfv.org/display/fds/FastDataStacks+Home
 [4]: http://info@frinx.io