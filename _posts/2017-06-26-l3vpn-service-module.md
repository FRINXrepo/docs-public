---
ID: 4776
post_title: L3VPN Service Module
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/l3vpn-service-module.html
published: true
post_date: 2017-06-26 10:10:28
---
The goal of this project is to automate provisioning of Layer 3 Virtual Private Network (L3VPN) on Service Provider (SP) routers.

This is done by using the Frinx ODL controller which configures routers based on intent of the L3VPN service. The Frinx ODL controller translates the L3VPN service abstraction to network element configuration. ![L3VPN Service][1]

The postman collection for the L3VPN service module can be accessed [here][2]

## A bit about L3VPN

### Problem definition and L3VPN

A company needs to reconnect multiple sites with each other via a Service Provider which provides L3 connectivity to the company. The company's sites exchange routing information and multiple companies may use overlapping address space so there is a need to isolate companies and their address spaces. L3VPN offers a solution for those requirements.

Host1 and Host2 are two different sites for the same company and they both connect to the Service Provider using a separate connection. They need to interconnect two of their sites.

![Two company's sites connected to SP][3]

In this case L3VPN provides site-to-site connectivity and the SP network behaves as a router between the company’s sites. The company’s routes are exchanged via the SP network. ![Solution with L3VPN between sites.][4]

### Terminology

The following terms are often used in the L3VPN domain:

*   **Customer Edge (CE)** device – router at customer site connected to SP
*   **Provider Edge (PE)** device – router at the edge of the SP network which provides connectivity for CE
*   **Provider (P)** device – core router on the SP network providing connectivity among PE routers

![Terminology in picture][5]

### Topologies

Common topologies used in L3VPN.

#### Any to Any

Sites can forward traffic directly among each other in a VPN. Communication is restricted to a particular VPN so it is not possible to communicate with sites on different VPNs. ![Any to Any topology example][6]

#### Hub and Spoke

Spoke sites in the VPN can communicate with each other only through the hub site. This is usually used when all sites must communicate through an access control device. ![Hub and Spoke topology example][7]

## L3VPN Provider

L3VPN Provider is an implementation which automatically provisions L3VPN on PE routers based on intended L3VPN service. It exposes a domain-specific API for L3VPN manipulation and declarative configuration “what vs how”.

L3VPN Provider supports network-wide transactions, which are transactions on top of multiple devices. Rollback of a network wide transaction means rollback of configuration on each device which was a part of the conifiguration. The rollback of a network-wide transaction is done automatically if there is failed configuration on at least one device.

### Use Case Specification

L3VPN Provider can be used on a network where:

*   Any to Any L3VPN topology is needed
*   CE - PE connection belongs to only one VPN
*   CE runs BGP for route advertising to PE

![Use case example][8]

### Architecture

L3VPN Provider is composed of multiple components. The high level architecture is shown in the picture below.

![Architecture][9]

An external application modifies *l3vpn-svc* in CONF DS. L3VPN can be configured on nodes which are read from *provider-edge-topology*. When all changes are done, the external application calls RPC *commit-l3vpn-svc*. The RPC reads the intended state from CONF DS, schedules processing, stores *status-l3vpn-provider* with "in-progress" status to OPER DS and then returns RPC output. L3VPN Provider creates a diff between *configured-l3vpn-svc* and *l3vpn-svc*. This diff is configured inside the network-wide transaction on the necessary PE routers by using particular Network Element Plugins.

If configuration of routers is successful then a new *configured-l3vpn-svc* is stored to OPER DS and status in *status-l3vpn-provider* is set to "complete". If configuration on one of the devices fails, the rollback of the network-wide transaction starts and *status-l3vpn-provider* is set to "rollback-in-progress".

If rollback is successful then *status-l3vpn-provider* has status "failed", otherwise the status is "inconsistent". The architecture can be extended very easily because Network Element Plugin needs to implement only NEP SPI, rollback, and network element registration. IOS NEP in the above picture is not implemented yet.

As has been mentioned, NEP registers network elements to L3VPN Provider. L3VPN Provider stores network elements as nodes to abstract topology *provider-edge-topolgoy* and this topology is a source of nodes which can be used for L3VPN configuration.

#### API description

The API is described using YANG modules. An external application can consume the API via RESTCONF, NETCONF, or JAVA. The L3VPN service module provides domain-specific abstraction where the abstraction describes attributes of VPNs and sites instead of configuration of network elements. The SDN controller translates the abstraction to network element configuration.

##### [ietf-l3vpn-svc@2017-05-02.yang][10]

The original YANG is from [RFC 8049][11]. Supported statements are shown in [generated UML from the original YANG][12]. This YANG module is modified in order to reuse its parts and is extended with L3VPN Provider elements - [modified ietf-l3vpn-svc YANG module][13]

The YANG module contains 3 root statements and one RPC:

*   **container l3vpn-svc** – represents intended state which is stored in CONF DS.
*   **container status-l3vpn-provider** – describes state of processing of L3VPN service which is processed or was processed by the L3VPN Provider. This state of processing is stored in OPER DS.
*   **container configured-l3vpn-svc** – shows last successfully configured L3VPN service.
*   **rpc commit-l3vpn-svc** – starts processing intent of L3VPN service. An output of RPC is the version which was assigned to the intent. The output is returned immediately after processing starts.

##### l3vpn-svc-aug@2017-05-02.yang

Augments ietf-l3vpn-svc module with statements which are needed for configuration of L3VPN - [l3vpn-svc-aug YANG module][14]

### Network Element Plugin

The Network Element Plugin (NEP) is a unit which implements SPI from the L3VPN Provider. The NEP is device API specific and is responsible for:

*   announcement of discovered device (PE) to the L3VPN Provider
*   translation between SPI Data Transfer Objects (DTO) and device configuration
*   rollback of configuration on a device

#### IOS-XRv Network Element Plugin

This plugin configures L3VPN on IOS-XRv using NETCONF. It listens on topology-netconf and announces PE capable devices to the L3VPN Provider. Rollback on a device is done automatically using the "Rollback-on-Error" capability.

![IOS-XRv NEP][15]

IOS-XRv NEP listens on nodes in *topology-netconf*. When a new IOS-XRv device is connected to Frinx ODL it appears as a new node in *topology-netconf* and IOS-XRv registers that node as PE to L3VPN Provider. If L3VPN Provider calls SPI in order to configure PEs via the IOS-XRv NEP, NETCONF is used for device configuration.

Here is an example of L3VPN configuration on IOS-XRv (parameters encapsulated in ** are specific for VPN or site):

    vrf **CE1**
     address-family ipv4 unicast
      import route-target
       **1:1**
      !
      export route-target
       **1:1**
      !
     !
    !
    
    
    interface **GigabitEthernet0/0/0/1**
     vrf **CE1**
     ipv4 address **192.168.1.1 255.255.255.0**
     no shut
    !
    
    
    router bgp **65000**
     !
     vrf **CE1**
      rd **1:1**
      address-family ipv4 unicast
       network **192.168.1.0/24**
      !
      neighbor **192.168.1.10**
       remote-as **65111**
       address-family ipv4 unicast
        route-policy **RPL_PASS_ALL** in
        route-policy **RPL_PASS_ALL** out
       !
      !
    !
    

NETCONF session configuration in IOS XR to allow ODL to connect:

    crypto key generate dsa
    crypto key generate rsa
    conf
    (config)#ssh server v2
    (config)#
    (config)#ssh server netconf port 830
    (config)#
    (config)#ssh timeout 120
    (config)#
    (config)#netconf-yang agent ssh
    (config)#
    (config)#ssh server netconf vrf default
    end
    

#### Mock Network Element Plugin

The purpose of this plugin is to mock functionality of the Network Element Plugin. It is used mainly for testing when you do not need to connect real devices. ![Mock NEP][16]

The Mock NEP listens on nodes from *mock-pe-topology*. When a node is created, the NEP registers this node as a PE node to the L3VPN Provider. When the L3VPN Provider calls the SPI which Mock NEP implements, instead of configuration of real devices, the SPI DTOs are stored under nodes in *mock-pe-topology* of OPER DS.

### Limitations

Implementation of L3VPN provider does not support all statements in ietf-l3vpn-svc@2017-05-02.yang. Unsupported statements can be found in YANG deviations.

[Inheritance of Parameters Defined at Site Level and Site Network Access Level][17] is not supported, therefore parameters must be defined at Site Network Access level. L3VPN Provider does not support reconciliation, therefore only L3VPN created via L3VPN Provider are visible through the API.

Other limitations:

*   only Any to Any topology is supported
*   CE - PE connection must belong to only one VPN
*   only BGP can be used between CE and PE
*   pre-configured MP-BGP between PE and BGP Route Reflector must exist
*   pre-configured Route Policy must exist

### User-facing features

#### odl-l3vpn-iosxrv

**Karaf installation:**

    feature:install odl-l3vpn-iosxrv   
    

**Description:**  
Installs L3VPN Provider with IOS-XRv NEP and NETCONF connector. This feature is NEP for IOS-XRv devices.

#### odl-l3vpn-testing

**Karaf installation:**

    feature:install odl-l3vpn-testing   
    

**Description:**  
Installs L3VPN Provider with Mock NEP and RESTCONF. This feature can be used for testing and demonstration purposes where real PE devices are not available.

The postman collection for the L3VPN service module can be accessed [here][2]

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
        FRINX 2.3.0
      </td>
      
      <td>
        VPN service module implementation with support for L3VPN and IOS XR (Version 6.1.2) NEP via NETCONF
      </td>
    </tr>
  </tbody>
</table>

 [1]: https://frinx.io/wp-content/uploads/2017/06/l3vpn_service.png "L3VPN Service"
 [2]: https://github.com/FRINXio/postman-collections
 [3]: https://frinx.io/wp-content/uploads/2017/06/problem.png "Example of problem"
 [4]: https://frinx.io/wp-content/uploads/2017/06/problem_solution.png "L3VPN between sites"
 [5]: https://frinx.io/wp-content/uploads/2017/06/terminology.png "Terminology in picture"
 [6]: https://frinx.io/wp-content/uploads/2017/06/topo_any-to-any.png "Any to Any topology"
 [7]: https://frinx.io/wp-content/uploads/2017/06/topo_hub-and-spoke.png "Hub and Spoke topology"
 [8]: https://frinx.io/wp-content/uploads/2017/06/use-case.png "Use case example"
 [9]: https://frinx.io/wp-content/uploads/2017/06/architecture.png "Architecture"
 [10]: https://frinx.io/frinx-documents/l3vpn-svc-aug2017-05-02-yang.html
 [11]: https://tools.ietf.org/html/rfc8049
 [12]: https://frinx.io/wp-content/uploads/2017/06/ietf-l3vpn-svc_uml.png "IETF UML"
 [13]: https://frinx.io/frinx-documents/ietf-l3vpn-svc2017-05-02-yang.html "ietf-l3vpn-svc@2017-05-02.yang"
 [14]: https://frinx.io/frinx-documents/l3vpn-svc-aug2017-05-02-yang.html "l3vpn-svc-aug@2017-05-02.yang"
 [15]: https://frinx.io/wp-content/uploads/2017/06/nep_ios-xrv.png "IOS-XRv NEP"
 [16]: https://frinx.io/wp-content/uploads/2017/06/nep_mock.png "Mock NEP"
 [17]: https://tools.ietf.org/html/rfc8049#section-6.3.2.3