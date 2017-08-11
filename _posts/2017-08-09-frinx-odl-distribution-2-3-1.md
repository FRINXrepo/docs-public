---
ID: 5355
post_title: Frinx ODL distribution 2.3.1
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-2-3-1.html
published: true
post_date: 2017-08-09 08:51:18
---
This document describes the latest changes, additions, known issues, and fixes for the Frinx ODL Distribution.<!--more-->

**Note that FRINX ODL distribution 2.3.1 requires Java 8**

#### New Features, Improvements

1.  L2VPN:
    
    *   new project introduced in 2.3.1

2.  L3VPN:
    
    Karaf L3VPN features are renamed in Frinx ODL 2.3.1:
    
    *   from odl-l3vpn-api to frinx-l3vpn-api
    *   from odl-l3vpn to frinx-l3vpn
    *   from odl-l3vpn-rest to frinx-l3vpn-rest
    *   from odl-l3vpn-testing to frinx-l3vpn-testing
    *   from odl-l3vpn-iosxrv to frinx-l3vpn-iosxrv 

3.  Renamed provider edge topology:
    
    *   from provider-edge-topology to l3vpn-provider-edge-topology

4.  GBP: Removed karaf features:
    
    *   odl-groupbasedpolicy-clustered
    *   odl-groupbasedpolicy-noop

5.  Fixed NETCONF IOS-XR capability check:
    
    *   Problem: Different versions of IOS-XR send capability with different string formating. 
    *   Solution: Checks only name of capability (YANG module) and revision instead of entire capability string.

6.  CLI plugin:
    
    *   Keepalive settings of CLI connection extracted into CLI node configuration
    *   Translate registry additional information: Actual YANG model nodes that are supported/implemented are listed for each YANG model
    *   Dry-run and journaling capabilities for CLI mountpoint: Enables users to write/read configuration to/from device as a dry-run operation to check what commands will ODL execute. Journal captures all executed commands for a CLI mountpoint and makes them visible for users. 

7.  IOS support:
    
    *   Openconfig interface YANG model support *Interface Configuration and State read/write support *Interface Ipv4 read/write support
    *   Openconfig BGP & RIB YANG model read support
    *   Initial custom interface YANG model removed

8.  Fixed boncycastle bundle order

9.  Fixed karaf restart after akka node becomes quarantined

#### Known Issues

1.  NETCONF: 
    *   MD-SAL clustering does not work correctly after temporary network isolation - one or more nodes can remain stuck in candidate state for all its shards.
2.  L2VPN: 
    *   L2VPN is not configured correctly when name in endpoint is the same for endpoints in different l2vpn-instances and these different endpoints are attached to same PE device.
3.  L3VPN: 
    *   RPC commit-l3vpn-svc fails when "l3vpn-svc-aug:route-distinguisher" attributes in vpn-service were updated(overwritten).

***Note - running feature:install frinx-l3vpn produces an error message, shown below. This error message is benign and can be ignored; l3vpn works as expected*  
Error message:**

2017-07-13 14:13:53,123 | ERROR | l for user karaf | lBundleScanningSchemaServiceImpl | 169 - org.opendaylight.controller.sal-schema-service - 1.4.3.Boron-SR3_2_3_0-frinxodl | Exception occured during invoking listener  
org.opendaylight.netconf.sal.restconf.impl.RestconfDocumentedException: errors: [RestconfError [error-type: application, error-tag: operation-failed, error-message: name doesn't exist.]] at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.findNodeInGroupings(RestconfMappingNodeUtil.java:369) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.addChildOfModuleBySpecificModule(RestconfMappingNodeUtil.java:350) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.addDeviationList(RestconfMappingNodeUtil.java:195) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.fillMapByModules(RestconfMappingNodeUtil.java:132) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.mapModulesByIetfYangLibraryYang(RestconfMappingNodeUtil.java:90) at org.opendaylight.restconf.handlers.SchemaContextHandler.onGlobalContextUpdated(SchemaContextHandler.java:63) at org.opendaylight.controller.sal.schema.service.impl.GlobalBundleScanningSchemaServiceImpl.notifyListeners(GlobalBundleScanningSchemaServiceImpl.java:156)

#### Opendaylight Boron Release Notes

The Frinx controller 2.3.1 is based on OpenDaylight Boron.

<https://wiki.opendaylight.org/view/Simultaneous_Release/Boron/Release_Notes>