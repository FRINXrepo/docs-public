---
ID: 4196
post_title: Frinx ODL distribution 2.2.1
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/frinx-odl-distribution-2-2-1.html
published: true
post_date: 2017-03-27 15:17:02
---
This document describes the latest changes, additions, known issues, and fixes for the Frinx Controller.<!--more-->[wpmem_form login]

**Note that FRINX ODL distribution 2.2.1 requires Java 8**

#### New Features, Improvements

1.  Added Radius authentication to the AAA project. 
2.  Fixed Angular dependency injections in the FRINX Feature Installer. 
3.  Fixed JUnits tests which were failing in Jenkins. 
4.  Changed naming of the ODL dependency versions. The pattern is now: major.minor.micro.classifier For example in the case of 0.7.2-Boron-SR2.2_2_1-frinxodl:  
    Major is: 0  
    Minor is: 7  
    Micro is: 2-Boron-SR2  
    Classifier is: 2_2_1-frinxodl  
    Previously, the classifier was of the format x-frinxodl, where x was an integer autoincremented with each release. 

#### Known Issues

1.  Clustering related issues with feature “odl-netconf-clustered-topology” – please use “odl-netconf-topology” instead.
2.  Netconf topology does not report connection issues – reports connected even if keepalive message is not received. Underlying connection reconnect functionality works as expected.

#### Opendaylight Boron Release Notes

The Frinx controller 2.2.1 is based on Opendaylight Boron.

<https://wiki.opendaylight.org/view/Simultaneous_Release/Boron/Release_Notes>

[/wpmem_form]