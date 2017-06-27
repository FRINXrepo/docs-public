---
ID: 1234
post_title: 'NETCONF: Intro'
author: frinxeditor
post_date: 2016-06-03 11:31:07
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/what-is-netconf-and-how-does-frinx-odl-distribution-use-netconf.html
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
#### What is NETCONF?

NETCONF is an Internet Engineering Task Force (IETF) protocol used to “create, recover, update, and delete configurations of network devices”. NETCONF operations are overlaid on the Remote Procedure Call (RPC) layer and may be described in either XML or JSON. An introduction to the IEFT working group and a summary of relevant RFCs and drafts is available at

<http://www.netconfcentral.org/> and the white paper included.

#### How does the Frinx ODL Distribution use NETCONF?

The Frinx ODL Distribution's southbound APIs use a NETCONF connector to communicate with downstream devices. The northbound APIs expose the YANG models of connected devices. This makes it possible to examine the operational and config datastores and to configure devices using RPCs. RESTCONF maps a subset of these YANG models to a RESTful interface.

**NETCONF – features used by the Frinx ODL Distribution include:** <img class="aligncenter wp-image-1286 size-full" src="https://frinx.io/wp-content/uploads/2016/06/3.png" alt="3" width="637" height="386" />