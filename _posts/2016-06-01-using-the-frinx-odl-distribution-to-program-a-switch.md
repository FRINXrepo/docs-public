---
ID: 762
post_title: Connecting to an OpenFlow switch
author: frinxeditor
post_date: 2016-06-01 14:43:08
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/using-the-frinx-odl-distribution-to-program-a-switch.html
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
In OpenDaylight, OpenFlow is implemented by the following features: odl-l2switch (and dependencies), openflowplugin and openflowjava. These can be installed in one of the following two ways:

**Option A: Installing Openflow features using the karaf console**  
Open or connect to a karaf console and type:

    feature:install odl-l2switch-all  
    feature:install odl-restconf  
    feature:install odl-mdsal-apidocs  
    feature:install odl-dlux-all  
    

(odl-dlux-all is installed by default)

**Option B: Installing Openflow features using the Frinx UI**  
Open the Web UI and navigate to: [http://localhost:8181/index.html#/featuremgr/index ][1]Use the filter functionality to verify which features are installed <img class="aligncenter wp-image-1282 size-large" src="https://frinx.io/wp-content/uploads/2016/06/1-1030x422.png" alt="1" width="1030" height="422" />   Verify that `odl-l2switch-all`, `odl-restconf`, `odl-mdsal-apidocs`, `odl-dlux-all` are installed. As shown in the screenshot above, an installed feature is indicated by both a tick in the Installed column and a trashcan in the Install/Uninstall column. The Frinx UI should be used when you wish to uninstall a feature, as uninstalling using the Karaf console is not currently supported and could cause undesirable behavior.

**Set up Mininet**  
The easiest way to do this is to download a mininet virtual machine (VM) from <https://github.com/mininet/mininet/wiki/Mininet-VM-Images> Then configure your environment so that you can connect to the Mininet VM from the machine hosting the Frinx controller. For example: if the Frinx ODL Distribution is hosted at 10.10.199.149 and Mininet is installed at 10.10.199.20, a ping should work in both directions.  
Use the following command to start Mininet, replacing < your controller ip > with the IP address of the machine hosting the Frinx controller.

    sudo mn --topo linear,3 --mac --controller=remote,ip=< your controller ip >,port=6633 --switch ovsk,protocols=OpenFlow13  
    

If the command is successful, then if you go to

<http://10.10.199.149:8181/index.html#/topology> you will see something like the screenshot below: <img class="aligncenter wp-image-1284 size-large" src="https://frinx.io/wp-content/uploads/2016/06/2-1030x620.png" alt="2" width="1030" height="620" /> The OpenDaylight userguide describes alternative ways to start mininet: [https://nexus.opendaylight.org/content/sites/site/org.opendaylight.docs/master/userguide/manuals/userguide/bk-user-guide/content/\_create\_a_network_using_mininet.html][2]

 [1]: http://localhost:8181/index.html#/featuremgr/index
 [2]: https://nexus.opendaylight.org/content/sites/site/org.opendaylight.docs/master/userguide/manuals/userguide/bk-user-guide/content/_create_a_network_using_mininet.html