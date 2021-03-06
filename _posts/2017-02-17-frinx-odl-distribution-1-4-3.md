---
ID: 3907
post_title: Frinx ODL distribution 1.4.3
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-1-4-3.html
published: true
post_date: 2017-02-17 09:00:47
---
This document describes the latest changes, additions, known issues, and fixes for the Frinx Controller. <!--more-->[wpmem_form login]

**Note that FRINX ODL distribution 1.4.3 requires Java 8**

#### New Features, Improvements

1.  The Daexim project has been backported from OpenDaylight to the FRINX distribution.
2.  Improved Alcatel-Lucent NETCONF support.
3.  Fixed a race condition in NETCONF topology which resulted in the operational datastore not being deleted when deleting the device from the config datastore.

#### Known Issues

1.  Clustering related issues with feature “odl-netconf-clustered-topology” – please use “odl-netconf-topology” instead.
2.  Netconf topology does not report connection issues – reports connected even if keepalive message is not received. Underlying connection reconnect functionality works as expected.

#### Opendaylight Beryllium SR4 Release Notes

The Frinx controller 1.4.3 is based on Opendaylight Beryllium SR4. Where a feature is present in both controllers, the same Release Notes apply

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