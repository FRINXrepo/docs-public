---
ID: 1238
post_title: 'NETCONF: Deleting a mounted device'
author: frinxeditor
post_date: 2016-06-03 11:35:08
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/deleting-the-mounted-netconf-device-2.html
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
This is done over RESTCONF using the HTTP Delete method. *HTTP Method: DELETE* *HTTP URL:* <http://localhost:8181/restconf/config/opendaylight-inventory:nodes/node/controller-config/yang-ext:mount/config:modules/module/odl-sal-netconf-connector-cfg:sal-netconf-connector/device> *HTTP Headers:* *Content-type: application/xml* *Accept: application/xml*

#### Next steps

The OpenDaylight user guide for NETCONF is still synched with the Lithium release. The current state of the NETCONF features is tracked at

<https://wiki.opendaylight.org/view/Weather>