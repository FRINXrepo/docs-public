---
ID: 2227
post_title: Frinx ODL distribution 1.2.6
author: ngray@frinx.io
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-1-2-6.html
published: true
post_date: 2016-08-31 13:49:58
---
This document describes the latest changes, additions, known issues, and fixes for the Frinx Controller.

<!--more-->[wpmem_form login]

## Additions

Added Kar Upload API to installer and other bundle APIs. See <a href="https://frinx.io/frinx-documents/using-the-frinx-api-bundle.html" target="_blank">this page</a> for more details Fixed cosmetic bugs in Installer's frontier

## Known Issues

#### The Kar Upload and other bundle APIs do not implement authentication

As such, we advise against using this functionality in a production environment at this stage.

## Opendaylight Beryllium SR2 Release Notes

The Frinx controller 1.2.6 is based on Opendaylight Beryllium SR2. Where a feature is present in both controllers, the same Release Notes apply

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes> odlparent <https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#ODL_Root_Parent>

yangtools

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#YANG_Tools>

mdsal

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#MD-SAL>

controller (without xsql)

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#Controller>

netconf

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#NETCONF>

aaa

[https://wiki.opendaylight.org/view/Simultaneous*Release/Beryllium/SR2/Release_Notes#Authentication.2C_Authorization_and_Accounting*.28AAA.29][1]

dlux

topoprocessing

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#Topology_Processing_Framework>

snmp

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#SNMP_Plugin>

openflowjava and openflowplugin

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#OpenFlow_Plugin>

neutron

[https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#Neutron_Northbound][2]

sfc

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#Service_Function_Chaining>

ovsdb (without netvirt)

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#OVSDB_Integration>

gbp

[https://wiki.opendaylight.org/view/Simultaneous*Release/Beryllium/SR2/Release_Notes#Group_Based_Policy*.28][3]

l2switch

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#L2_Switch>

bgpcep

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#BGP_PCEP>

lispflowmapping

<https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#LISP_Flow_Mapping>

[/wpmem_form]

 [1]: https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#Authentication.2C_Authorization_and_Accounting_.28AAA.29
 [2]: https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#OpenFlow_Plugin
 [3]: https://wiki.opendaylight.org/view/Simultaneous_Release/Beryllium/SR2/Release_Notes#Group_Based_Policy_.28