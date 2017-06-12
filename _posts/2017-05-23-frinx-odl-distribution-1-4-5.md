---
ID: 4504
post_title: Frinx ODL distribution 1.4.5
author: frinxadmin
post_date: 2017-05-23 14:13:38
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-1-4-5.html
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

**Note that FRINX ODL distribution 1.4.5 requires Java 8**

#### New Features, Improvements

1.  Daexim: Created exactly one transaction per Daexim import
2.  Restconf: Changed URI decoding from ISO-8859-1 to UTF-8
3.  GBP: Added feature odl-groupbasedpolicy-noop which is without registration listener
4.  GBP: Exposed resolve-policy via RPC registry
5.  GBP: Added PolicyValidatorRegistry#updateAllTenants
6.  GBP: Implemented unregister l3-prefix endpoint.
7.  GBP: Fixed NPE in MatcherUtils
8.  GBP: Make subject selection in parallel
9.  GBP: Added method PolicyResolverUtils.resolvePolicyOnlyForEpgs 

#### Known Issues

1.  Clustering related issues with feature “odl-netconf-clustered-topology” – please use “odl-netconf-topology” instead.
2.  Netconf topology does not report connection issues – reports connected even if keepalive message is not received. Underlying connection reconnect functionality works as expected.

#### Opendaylight Beryllium SR4 Release Notes

The Frinx controller 1.4.5 is based on Opendaylight Beryllium SR4. Where a feature is present in both controllers, the same Release Notes apply

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