---
ID: 2482
post_title: Frinx ODL distribution 1.4.0
author: frinxadmin
post_date: 2016-11-04 20:00:05
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-1-4-0.html
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
This document describes the latest changes, additions, known issues, and fixes for the Frinx Controller. <!--more-->[wpmem_form login]

#### New Features, Improvements

1.  <span class="line">Added new netconf API and ALU/SROS specific customization</span>
2.  <span class="line">GBP-base now cluster aware -  Cluster awareness is achieved through the use of the Entity Ownership Service -  ClusteredPolicyResolver has been created as a clustered version of PolicyResolver -  The new karaf feature "odl-groupbasedpolicy-clustered" runs a clustered version of policy resolver and endpoint registry1. <em>Note: Feature "odl-groupbasedpolicy-clustered" must be installed instead of feature "odl-groupbasedpolicy-base" when ODL is run on more than one cluster node</em></span>
3.  Fixed bug for keepalive in "odl-netconf-clustered-topology"

#### Known Issues

1.  Clustering related issues with netconf (feature "odl-netconf-clustered-topology") -  Node does not always reconnect after temporal isolation -  Occasionally the netconf connection between one or more nodes and the netconf device is not established or is dropped after the hello message is transmitted.

#### Opendaylight Beryllium SR4 Release Notes

The Frinx controller 1.4.0 is based on Opendaylight Beryllium SR4. Where a feature is present in both controllers, the same Release Notes apply

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes>  
odlparent <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#ODL_Root_Parent>  
yangtools <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#YANG_Tools>  
mdsal <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#MD-SAL>  
controller (without xsql) <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#Controller>  
netconf <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#NETCONF>  
aaa [https://wiki.opendaylight.org/view/SimultaneousRelease/Beryllium/SR4/Release_Notes#Authentication.2C_Authorization_and_Accounting.28AAA.29][1]  
dlux topoprocessing <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#Topology_Processing_Framework>  
snmp <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#SNMP_Plugin>  
openflowjava and openflowplugin <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#OpenFlow_Plugin>  
neutron [https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#Neutron_Northbound][2]  
sfc <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#Service_Function_Chaining>  
ovsdb (without netvirt) <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#OVSDB_Integration>  
gbp [https://wiki.opendaylight.org/view/Simultaneous*Release/Beryllium/SR4/Release_Notes#Group_Based_Policy*.28][3]  
l2switch <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#L2_Switch>  
bgpcep <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#BGP_PCEP>  
lispflowmapping <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#LISP_Flow_Mapping> [/wpmem_form]

 [1]: https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#Authentication.2C_Authorization_and_Accounting_.28AAA.29
 [2]: https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#OpenFlow_Plugin
 [3]: https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR4/Release_Notes#Group_Based_Policy_.28