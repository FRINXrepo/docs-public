---
ID: 766
post_title: >
  Using NETCONF with the Frinx ODL
  Distribution
author: frinxeditor
post_date: 2016-06-01 14:44:24
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/using-netconf-with-the-frinx-odl-distribution.html
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
[wpmem_form login] 
# Using NETCONF with the Frinx ODL Distribution

### What is NETCONF? NETCONF is an IETF protocol which is used to “create, recover, update, and delete configurations of network devices”. NETCONF operations are overlaid on Remote Procedure Call (RPC) layer and may be described in either XML or JSON An introduction to the IEFT working group and a summary of relevant RFCs and drafts is available at 

<http://www.netconfcentral.org/> and the white paper included. 
### How does Frinx ODL Distribution use NETCONF? The Frinx ODL Distributions southbound APIs use a NETCONF connector to communicate with downstream devices. The northbound APIs expose the YANG models of connected devices. This makes it possible to examine the operational, config datastores and to configure the device using RPCs. RESTCONF maps a subset of these YANG models to a RESTful interface. 

**NETCONF – features used by the Frinx ODL Distribution include:** <img class="aligncenter wp-image-1286 size-full" src="https://frinx.io/wp-content/uploads/2016/06/3.png" alt="3" width="637" height="386" /> 
### Setting up a simple NETCONF session by mounting a device In this example we connect the controller to itself to verify that that NETCONF features were installed correctly. It is similar to loopback but done over a NETCONF session. After mounting itself, the YANG model of the Frinx ODL Distribution is exposed by RESTCONF and is an interesting point to begin exploring. 

#### Step 1 Install Features This can be done using either the Frinx ODL Distribution feature manager at 

<http://localhost:8181/index.html#/featuremgr/index> or the Karaf CLI as shown below 
     frinx-user@root> feature:install odl-restconf
     frinx-user@root> feature:install odl-netconf-connector-all
    

#### Step 2 Wait Until controller-config Is Connected Send a GET request to mount the controller using RESTCONF 

<http://localhost:8181/restconf/operational/opendaylight-inventory:nodes/node/controller-config> 
#### Step 3 Verify connection was successful Examine the HTTP response there should be a 200 status code and the text string 

*netconf-node-inventory:connected":true* 
### Deleting the mounted NETCONF device This is done over RESTCONF using HTTP Delete method. 

*HTTP Method: DELETE* *HTTP URL:* <http://localhost:8181/restconf/config/opendaylight-inventory:nodes/node/controller-config/yang-ext:mount/config:modules/module/odl-sal-netconf-connector-cfg:sal-netconf-connector/device> *HTTP Headers:* *Content-type: application/xml* *Accept: application/xml* 
### Next steps The OpenDaylight user guide for NETCONF is still synched with Lithium release. The current state of the NETCONF features is tracked at 

<https://wiki.opendaylight.org/view/Weather> [/wpmem_form]