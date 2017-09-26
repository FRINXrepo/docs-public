---
ID: 3951
post_title: Frinx ODL distribution 2.2.0
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-2-2-0.html
published: true
post_date: 2017-02-23 13:07:55
---
This document describes the latest changes, additions, known issues, and fixes for the Frinx Controller.<!--more-->[wpmem_form login]

**Note that FRINX ODL distribution 2.2.0 requires Java 8**

#### New Features, Improvements

1.  The Daexim project has been backported from OpenDaylight to the FRINX distribution.
2.  Improved Alcatel-Lucent NETCONF support.
3.  Fixed a race condition in NETCONF topology which resulted in the operational datastore not being deleted when deleting the device from the config datastore.

#### Known Issues

1.  Clustering related issues with feature “odl-netconf-clustered-topology” – please use “odl-netconf-topology” instead.
2.  Netconf topology does not report connection issues – reports connected even if keepalive message is not received. Underlying connection reconnect functionality works as expected.

#### Opendaylight Boron Release Notes

The Frinx controller 2.2.0 is based on Opendaylight Boron.

<https://wiki.opendaylight.org/view/Simultaneous_Release/Boron/Release_Notes>

[/wpmem_form]