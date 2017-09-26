---
ID: 3002
post_title: Frinx ODL distribution 1.4.1
author: ngray@frinx.io
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-1-4-1.html
published: true
post_date: 2016-11-22 09:12:33
---
This document describes the latest changes, additions, known issues, and fixes for the Frinx Controller. <!--more-->[wpmem_form login]

#### New Features, Improvements

1.  <span class="line">Basic clustering on top of odl-netconf-topology: Fixed optimistic locking issues implementing retry mechanism in odl-netconf-topology to allow this feature to be run in cluster.</span>

#### Known Issues

1.  Clustering related issues with feature "odl-netconf-clustered-topology" - please use "odl-netconf-topology" instead.
2.  Netconf topology [1][1] does not report connection issues - reports connected even if keepalive message is not received. Underlying connection reconnect functionality works as expected. [1][1]: available via restconf URL http://${ODL_HOST}:8181/restconf/operational/network-topology:network-topology/topology/topology-netconf/

#### Opendaylight Beryllium SR4 Release Notes

The Frinx controller 1.4.1 is based on Opendaylight Beryllium SR4. Where a feature is present in both controllers, the same Release Notes apply

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