---
ID: 4561
post_title: General
author: frinxadmin
post_date: 2017-05-29 13:03:15
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-vpp-distribution/vpp-operations-manual/howto-general.html
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
**Dump VPP message table**

Vpp APIs work with messages, to check all the available messages and their indices use in VAT:

    dump_msg_api_table
    

**View VPP node graph**

VPP is implemented as a set of ordered graph nodes, to see them live, use following command in CLI:

    show vlib graph
    

**Trace VPP's API executions**

To record the execution of its APIs, use following command outside of VPP:

    sudo vppctl api trace save demo.api && sudo vppctl api trace custom-dump /tmp/demo.api