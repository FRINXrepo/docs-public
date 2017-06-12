---
ID: 749
post_title: FRINX ODL DISTRIBUTION OVERVIEW
author: frinxeditor
post_date: 2016-06-01 14:40:14
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-overview.html
published: true
sidebar:
  - 'a:1:{i:0;s:0:"";}'
footer:
  - 'a:1:{i:0;s:0:"";}'
header_title_bar:
  - 'a:1:{i:0;s:0:"";}'
header_transparency:
  - 'a:1:{i:0;s:0:"";}'
---
[wpmem_form login] **Vendor Agnostic** By design the Frinx ODL Distribution is vendor agnostic. The ability to model-data and to dynamically load java classes means that any protocol model-able in YANG is supportable. Example implementations of protocols include OpenFlow, PCEP and SNMP. **Model-driven** The Frinx ODL Distribution is model-driven, the network and operations performed on it are modeled in YANG. The YANG data structures are shared using operational and config datastores. The datastores are accessible via RESTCONF and NETCONF. **Future Proof** MD-SAL allows any application to be bundled as a service and loaded into the controller. These services can be configured and inter connected to solve complex problems and adapt to a changing network. This means the Frinx ODL Distribution is future proofed. **Extensible** The microservices architecture enables control of protocols, plug-ins and applications and the connection of external consumers and providers. More than 50 OpenDaylight projects extend Frinx’s network functionality by bundling services and functionality as Karaf features. Karaf features are a hierarchy of OSGI bundles, ready for plugin to Frinx‘s OSGI container. [/wpmem_form]