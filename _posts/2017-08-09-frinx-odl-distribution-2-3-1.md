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

1.  Features l2vpn and l3vpn has been renamed in Boron 2.3.1. Instead of odl-* naming is now frinx-* (frinx-l2vpn...) 

#### Known Issues

1.  After node isolation netconf clustering does not function correctly
2.  GBP-features odl-groupbasedpolicy-clustered and odl-groupbasedpolicy-noop does not function correctly

***Note - running feature:install odl-l3vpn produces an error message, shown below. This error message is benign and can be ignored; l3vpn works as expected*  
Error message:**

2017-07-13 14:13:53,123 | ERROR | l for user karaf | lBundleScanningSchemaServiceImpl | 169 - org.opendaylight.controller.sal-schema-service - 1.4.3.Boron-SR3_2_3_0-frinxodl | Exception occured during invoking listener  
org.opendaylight.netconf.sal.restconf.impl.RestconfDocumentedException: errors: [RestconfError [error-type: application, error-tag: operation-failed, error-message: name doesn't exist.]] at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.findNodeInGroupings(RestconfMappingNodeUtil.java:369) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.addChildOfModuleBySpecificModule(RestconfMappingNodeUtil.java:350) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.addDeviationList(RestconfMappingNodeUtil.java:195) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.fillMapByModules(RestconfMappingNodeUtil.java:132) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.mapModulesByIetfYangLibraryYang(RestconfMappingNodeUtil.java:90) at org.opendaylight.restconf.handlers.SchemaContextHandler.onGlobalContextUpdated(SchemaContextHandler.java:63) at org.opendaylight.controller.sal.schema.service.impl.GlobalBundleScanningSchemaServiceImpl.notifyListeners(GlobalBundleScanningSchemaServiceImpl.java:156)

#### Opendaylight Boron Release Notes

The Frinx controller 2.3.1 is based on OpenDaylight Boron.

<https://wiki.opendaylight.org/view/Simultaneous_Release/Boron/Release_Notes>