---
ID: 5004
post_title: Frinx ODL distribution 2.3.0
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-2-3-0.html
published: true
post_date: 2017-07-12 13:54:06
---
This document describes the latest changes, additions, known issues, and fixes for the Frinx Controller.<!--more-->

**Note that FRINX ODL distribution 2.3.0 requires Java 8**

#### New Features, Improvements

1.  Added CLI service module to enable the controller to manage devices over a CLI 
2.  Added L3VPN for automated provisioning of Layer 3 Virtual Private Networks (L3VPN) on Service Provider (SP) routers

#### Known Issues

1.  After node isolation netconf clustering does not function correctly
2.  GBP-features odl-groupbasedpolicy-clustered and odl-groupbasedpolicy-noop does not function correctly

*Note - running feature:install odl-l3vpn produces an error, shown below. This error message is benign; l3vpn works as expected* Error message:

    2017-07-13 14:13:53,123 | ERROR | l for user karaf | lBundleScanningSchemaServiceImpl | 169 - org.opendaylight.controller.sal-schema-service - 1.4.3.Boron-SR3_2_3_0-frinxodl | Exception occured during invoking listener org.opendaylight.netconf.sal.restconf.impl.RestconfDocumentedException: errors: [RestconfError [error-type: application, error-tag: operation-failed, error-message: name doesn't exist.]] at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.findNodeInGroupings(RestconfMappingNodeUtil.java:369) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.addChildOfModuleBySpecificModule(RestconfMappingNodeUtil.java:350) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.addDeviationList(RestconfMappingNodeUtil.java:195) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.fillMapByModules(RestconfMappingNodeUtil.java:132) at org.opendaylight.restconf.utils.mapping.RestconfMappingNodeUtil.mapModulesByIetfYangLibraryYang(RestconfMappingNodeUtil.java:90) at org.opendaylight.restconf.handlers.SchemaContextHandler.onGlobalContextUpdated(SchemaContextHandler.java:63) at org.opendaylight.controller.sal.schema.service.impl.GlobalBundleScanningSchemaServiceImpl.notifyListeners(GlobalBundleScanningSchemaServiceImpl.java:156)
    

#### Opendaylight Boron Release Notes

The Frinx controller 2.3.0 is based on Opendaylight Boron.

<https://wiki.opendaylight.org/view/Simultaneous_Release/Boron/Release_Notes>