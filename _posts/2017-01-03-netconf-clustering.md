---
ID: 3425
post_title: NETCONF Clustering
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/netconf-clustering.html
published: true
post_date: 2017-01-03 12:13:47
---
Follow the steps below in order to configure NETCONF. Note that it doesn't matter whether you are running on a single node or a cluster - the steps are the same. If you are running a cluster then simply enter these commands on ogene of the cluster nodes and that node will pass the information to the other nodes.

**Netconf mount**  
Before we can add the NETCONF device we must configure a set of parameters (via the command line). Enter the following commands in a terminal, using the values that are relevant for your particular case.

    NETCONF_NAME [Name of the NETCONF mountpoint inside OpenDaylight]  
    NETCONF_HOST [IP address of the NETCONF device]  
    NETCONF_PORT [Port used by the NETCONF device for communication with OpenDaylight]  
    NETCONF_USER [NETCONF device username]  
    NETCONF_PASS [NETCONF device password]
    

**Add device via mdsal's netconf topology**  
Before you can add a device you must install one of the following OpenDaylight features:

odl-netconf-topology  
odl-netconf-clustered-topology

Then run the following curl command from a terminal, replacing the variables e.g. '${NETCONF_NAME}' with the values you configured in the previous step (Netconf mount)

    curl --user admin:admin -v -X PUT "http://${ODL_HOST}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/${NETCONF_NAME}" -H "Content-Type: application/xml" -d '  
    <node xmlns="urn:TBD:params:xml:ns:yang:network-topology"> <node-id>'${NETCONF_NAME}'</node-id>     
    <host xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_HOST}'</host>  
    <port xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_PORT}'</port>  
    <username xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_USER}'</username>  
    <password xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_PASS}'</password>  
    <tcp-only xmlns="urn:opendaylight:netconf-node-topology">false</tcp-only>  
    <keepalive-delay xmlns="urn:opendaylight:netconf-node-topology">10</keepalive-delay>  
    <connection-timeout-millis xmlns="urn:opendaylight:netconf-node-topology">1000</connection-timeout-millis>  
    <default-request-timeout-millis xmlns="urn:opendaylight:netconf-node-topology">1000</default-request-timeout-millis> </node>'`
    

Now that the device has been added, you can interrogate it using the RESTCONF service provided by MD-SAL (OpenDaylight's Model-driven Service Abstraction Layer). A straightforward way to use the RESTCONF service is to use curl commands from the command line. Various commands can be used, for various purposes. We list these below. We also provide examples of these commands and the responses they generate. You can run these examples if you install the toaster feature in karaf. The idea of the toaster feature is to provide an example (based on a toaster and the functions it implements) to show you how to run various commands. To install the toaster feature, run OpenDaylight and then enter the following command on the karaf commandline:

     feature:install odl-toaster
    

**Getting config data from device**

To retrieve configuration data from the remote NETCONF device, use the following command in a terminal, replacing ${ODL_HOST} with the IP address of the machine on which you are running the FRINX OpenDaylight distribution.

    curl --user admin:admin -v "http://${ODL_HOST}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/${NETCONF_NAME}/yang-ext:mount/?prettyPrint=true" -H "Content-Type: application/yang.data+json"
    

Toaster example command:

    curl --user admin:admin -v "http://$ODL_HOST:8181/restconf/config/toaster:toaster/?prettyPrint=true"
    

Toaster example response:

    {
        "toaster": {
            "darknessFactor": 2000
        }
    }
    

**Getting operational data from device** *(SROS does not support this. For SROS devices, see the end of this document)*  
Similar to the above command, but extracts operational rather than config data. Again, replace ${ODL_HOST} with the IP address of the machine on which you are running the FRINX OpenDaylight distribution.

    curl --user admin:admin -v "http://${ODL_HOST}:8181/restconf/operational/network-topology:network-topology/topology/topology-netconf/node/${NETCONF_NAME}/yang-ext:mount/?prettyPrint=true" -H "Content-Type: application/yang.data+json"
    

Toaster example command:

    curl --user admin:admin -v "http://$ODL_HOST:8181/restconf/operational/toaster:toaster/?prettyPrint=true"
    

Toaster example response:

    {
        "toaster": {
            "toasterManufacturer": "Opendaylight",
            "toasterModelNumber": "Model 1 - Binding Aware",
            "toasterStatus": "up"
        }
    }
    

**Getting a list of netconf devices + their connection status**  
Replace ${ODL_HOST} with the IP address of the machine on which you are running the FRINX OpenDaylight distribution.

    curl --user admin:admin -v "http://${ODL_HOST}:8181/restconf/operational/network-topology:network-topology/topology/topology-netconf/?prettyPrint=true"
    

**Deleting device**  
To delete the remote NETCONF device from OpenDaylight, enter the following command in a terminal, replacing ${ODL_HOST} with the IP address of the machine on which you are running the FRINX OpenDaylight distribution.

    curl --user admin:admin -X DELETE "http://${ODL_HOST}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/${NETCONF_NAME}" -v
    

## Vendor/device specific implementations

**Using SROS 13**  
To configure netconf, use following restconf call. Note the first line below (which configures the IP of the machine hosting the FRINX OpenDaylight distribution) should be edited as required. Within the first line of the curl command, replace ${ODL_HOST} with the IP address of the machine on which the FRINX OpenDaylight distribution is running: :

    ODL_HOST=127.0.0.1 # change this accordingly
    
    curl --user admin:admin -v  -X PUT "http://${ODL_HOST}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/${NETCONF_NAME}" -H "Content-Type: application/xml" -d '                                                        
    <node xmlns="urn:TBD:params:xml:ns:yang:network-topology">
       <node-id>'${NETCONF_NAME}'</node-id>
       <host xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_HOST}'</host>
       <port xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_PORT}'</port>
       <username xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_USER}'</username>
       <password xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_PASS}'</password>
       <tcp-only xmlns="urn:opendaylight:netconf-node-topology">false</tcp-only>
       <keepalive-delay xmlns="urn:opendaylight:netconf-node-topology">10</keepalive-delay>
       <yang-module-capabilities xmlns="urn:opendaylight:netconf-node-topology">
          <capability>urn:ietf:params:xml:ns:yang:ietf-inet-types?module=ietf-inet-types&amp;revision=2010-09-24</capability>
          <capability>urn:ietf:params:xml:ns:netconf:base:1.0?module=ietf-netconf&amp;revision=2011-06-01</capability>
       </yang-module-capabilities>
       <customization-factory xmlns="urn:opendaylight:netconf-node-topology">netconf-customization-alu</customization-factory>   
     </node>'
    

The only difference between normal configuration and this is the customization factory and 2 added capabilities that are missing in hello message.

**Using SROS 140R04**  
For this version, use `netconf-customization-alu-ignore-candidate` as customization factory. The purpose of the customization is to ensure that the response from the SROS device is in the required format.

To configure the mountpoint for SROS 14, enter the following command, replacing ${ODL_HOST} with the IP address of the machine on which the FRINX OpenDaylight distribution is running:

    curl --user admin:admin -v  -X PUT "http://${ODL_HOST}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/${NETCONF_NAME}" -H "Content-Type: application/xml" -d '                                                        
    <node xmlns="urn:TBD:params:xml:ns:yang:network-topology">
       <node-id>'${NETCONF_NAME}'</node-id>
       <host xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_HOST}'</host>
       <port xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_PORT}'</port>
       <username xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_USER}'</username>
       <password xmlns="urn:opendaylight:netconf-node-topology">'${NETCONF_PASS}'</password>
       <tcp-only xmlns="urn:opendaylight:netconf-node-topology">false</tcp-only>
       <keepalive-delay xmlns="urn:opendaylight:netconf-node-topology">10</keepalive-delay>
       <yang-module-capabilities xmlns="urn:opendaylight:netconf-node-topology">
          <capability>urn:ietf:params:xml:ns:yang:ietf-inet-types?module=ietf-inet-types&amp;revision=2010-09-24</capability>
    
          <capability>urn:nokia.com:sros:ns:yang:sr:conf?module=nokia-conf-log&amp;revision=2016-07-11</capability>
          <capability>urn:nokia.com:sros:ns:yang:sr:conf?module=nokia-conf-python&amp;revision=2016-07-11</capability>
          <capability>urn:nokia.com:sros:ns:yang:sr:conf?module=nokia-conf-qos&amp;revision=2016-07-15</capability>
          <capability>urn:nokia.com:sros:ns:yang:sr:conf?module=nokia-conf-service&amp;revision=2016-07-13</capability>
          <capability>urn:nokia.com:sros:ns:yang:sr:conf?module=nokia-conf-system&amp;revision=2016-07-13</capability>
    
       </yang-module-capabilities>
       <customization-factory xmlns="urn:opendaylight:netconf-node-topology">netconf-customization-alu-ignore-candidate</customization-factory>   
     </node>
    '
    

<table>
  <thead>
    <tr>
      <th>
        Feature Guide
      </th>
      
      <th>
      </th>
      
      <th>
      </th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <td>
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
      </td>
      
      <td>
      </td>
      
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        Feature introduced in
      </td>
      
      <td>
        FRINX 1.4.1
      </td>
      
      <td>
        NETCONF clustering module
      </td>
    </tr>
  </tbody>
</table>