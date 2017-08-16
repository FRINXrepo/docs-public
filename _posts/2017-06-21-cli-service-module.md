---
ID: 4750
post_title: CLI Service Module User Guide
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/cli-service-module.html
published: true
post_date: 2017-06-21 10:46:36
---
*The Postman collection for the CLI service module can be accessed [here][1]. (latest version: FRINX CLI 2.3.1.postman_collection.json). It contains several pre-configured REST calls for mounting and interacting with devices, which can be edited for your use (by changing IP addresses, port numbers etc). We refer to the postman collection in the usage section below* **Postman can be downloaded for free [here][2]**

## Introduction

The CLI southbound plugin enables the FRINX Opendaylight distribution to communicate with CLI devices that do not speak NETCONF or any other programmatic API. The CLI service module uses YANG models and implements a translation logic to send and receive structured data to and from CLI devices. This allows applications to use a service model or unified device model to communicate with a broad range of network platforms and SW revisions from different vendors.

Much like the NETCONF southbound plugin, the CLI southbound plugin enables fully model-driven, transactional device management for internal and external OpenDaylight applications. In fact, the applications are completely unaware of underlying transport and can manage devices over the CLI plugin in the same exact way as over NETCONF.

Once we have mounted the device, we can present an abstract, model-based network device and service interface to applications and users. For example, we can parse the output of an IOS command and return structured data.

![CLI southbound plugin][3]

## Architecture

This section provides an architectural overview of the plugin, focusing on the main conponents.

### CLI topology

The CLI topology is a dedicated topology instance where users and applications can:

*   mount a CLI device 
*   unmount a device 
*   check the state of connection 
*   read/write data from/to a device 
*   execute RPCs on a device 

In fact, this topology can be seen as an equivalent of topology-netconf, providing the same features for netconf devices.

#### APIs

The topology APIs are YANG APIs based on the ietf-topology model. Similarly to netconf topology, CLI topology augments the model with some basic configuration data and also some state to monitor mountpoints. For details please refer to the latest CLI topology YANG model.

### CLI mountpoint

The plugin relies on MD-SAL and its concept of mountpoints to expose management of a CLI device into Opendaylight. By exposing a mountpoint into MD-SAL, it enables the CLI topology to actually access the device's data in a structured/YANG manner. Components of such a mountpoint can be divided into 3 distinct layers:

*   Service layer - implementation of MD-SAL APIs delegating execution to transport layer.
*   Translation layer - a generic and extensible translation layer. The actual translation between YANG and CLI takes place in the extensions. The resulting CLI commands are then delegated to transport layer.
*   Transport layer - implementation of various transport protocols used for actual communication with network devices.

The following diagram shows the layers of a CLI mountpoint:

![CLI mountpoint][4]

#### APIs

The mountpoint exposes standard APIs and those are:

*   DataBroker
*   RpcService
*   and (optionally) a NotificationService

These are the basic APIs every mountpoint in MD-SAL needs to provide. The actual data consumed and provided by the services depends on the YANG models implemented for a particular device type.

#### Translation layer

The CLI southbound plugin is as generic as possible. However, the device-specific translation code (from YANG data -> CLI commands and vice versa), needs to be encapsulated in a device-specific translation plugin. E.g. Cisco IOS specific translation code needs to be implemented by Cisco IOS translation plugin before Opendaylight can manage IOS devices. These translation plugins in conjunction with the generic translation layer allow for a CLI mountpoint to be created.

##### Device specific translation plugin

Device specific translation plugin is a set of: - YANG models  
- Data handlers  
- RPC implementations

that actually

*   defines the model/structure of the data in Opendaylight 
*   implements the translation between YANG data and device CLI in a set of handlers 
*   (optionally) implements the translation between YANG rpcs and device CLI 

So the plugin itself is responsible for defining the mapping between YANG and CLI. However, the translation layer into which it plugs in is what handles the heavy lifting for it e.g. transactions, rollback, config data storage, reconciliation etc. Additionally, the SPIs of the translation layer are very simple to implement because the translation plugin only needs to focus on the translations between YANG <-> CLI.

###### Units

In order to enable better extensibility of the translation plugin and also to allow the separation of various aspects of a device's configuration, a plugin can be split into multiple units. Where a unit is actually just a subset of a plugin's models, handlers and RPCs.

A single unit will usually cover a particular aspect of device management e.g. the interface management unit.

Units can be completely independent or they can build on each other, but in the end (in the moment where a device is being mounted) they form a single translation plugin.

Each unit has to be registered under a specific device type(s) e.g. an interface management unit could be registered for various versions of the IOS device type. When mounting an IOS device, the CLI southbound plugin collects all the units registered for the IOS device type and merges them into a single plugin enabling full management.

The following diagram shows an IOS device translation plugin split into multiple units:

![IOS translation plugin][5]

#### Transport layer

There are various transport protocols available such as:

*   SSH 
*   Telnet 

But all of them implement the same APIs, which enables the translation layer of the CLI plugin to be completely independent of the underlying protocol in use. Deciding which transport will be used to manage a particular device is simply a matter of configuration.

## Data processing

There are 2 types of data in the Opendaylight world: Config and Operational. This section details how these data types map to CLI commands.

Just as there are 2 types of data, there are 2 streams of data in the CLI southbound plugin:

*   **Config**  
    *   user/application intended configuration for the device 
    *   translation plugins/units need to handle this configuration in data handlers as C(reate), U(pdate) and D(elete) operations - these data flow only towards the device - these data are cached in the mountpoint so when application performs read Config, it gets the cached version

![Config data][6]

*   **Operational** 
    *   actual configuration on the device
    *   optionally statistics from the device
    *   translation plugins/units need to pull these data out of the device when R(ead) operation is requested

![Operational data][7]

*   **RPCs** stand on their own and can actually encapsulate any command(s) on the device.

### Transactions and revert

As mentioned before, configuring a device is performed within transactions. If it's impossible to perform device configuration, the user/app facing transaction is failed and a revert procedure is initiated (in case there was partial configuration already submitted to the device).

### Reconciliation

There might be situations where there are inconsistencies between actual configuration on the device and the state cached in Opendaylight. That's why a reconciliation mechanism was developed to:

*   Allow the mountpoint to sync its state when first connecting to the device
*   Allow apps/users to request synchronization when an inconsistent state is expected e.g. manual configuration of the device

## Usage

This section provides samples for how to use the CLI southbound plugin to manage a particular device.

### Features

Install the following features into a running FRINX OpenDaylight instance (For running Frinx OpenDaylight, please see our [guide][8]):

    feature:install cli-topology cli-southbound-unit-ios odl-restconf
    

This installs the CLI topology, a baseline translation unit and an IOS essential unit.

### Logs

If finer logging is required, use the following command to enable DEBUG/TRACE logging:

    log:set TRACE io.frinx.cli
    

### Mounting a CLI device

The following sequence of operations needs to happen from the point when Opendaylight is configured to mount a CLI device until it is truly accessible for users and applications:

1.  Submit CLI device configuration into CLI topology 
    *   Over REST, NETCONF or from within Opendaylight
2.  CLI topology opens transport layer by opening a session with the device
3.  CLI topology collects all the units into a plugin and instantiates translation layer
4.  CLI topology builds mountpoint services on top of the translation layer
5.  CLI topology exposes the mountpoint into MD-SAL
6.  CLI topology updates operational state of this node in CLI topology to connected

#### Mounting and managing Generic Linux VM devices over REST

Please refer to the Postman collection available [here][1], folder *Linux mount*

#### Mounting and managing IOS devices over REST

Please refer to the Postman collection available [here][1], folder *Ios mount*.

Once you import the collection into Postman, open the Ios mount folder. You will see there are two calls available for mounting an Ios device: **Mounting by telnet:**

![telnet mount][9]

**Mounting by ssh** ![aah mount][10]

Now we can parse the output of an IOS command and return structured data.

IOS devices can also be mounted and managed from an application. For instructions, please see the end of the [Developer Guide][11]

## Supported devices

Please see [here][12] for a structured list of device types currently supported by the CLI southbound plugin and configuration aspects implemented for them.

It is possible to check a current list of units and thus a current list of supported devices directly from OpenDaylight's REST interface. Please refer to Postman collection available [here][1], folder *registry* for the call which displays the actual list.

More details regarding IOS and generic devices follow:

### IOS

IOS device management is supported. Currently supported aspects:

*   interface management 
*   VRF management 
*   Version data read 

### Generic device

It is possible to mount any network device as a generic device. This allows invocation of any commands on the device using RPCs, which return the output back as freeform data and it is up to user/application to make sense of them.

## Interaction with a CLI device

For a hands-on tour of the CLI plugin from within your browser, please try our [playground][13]

<table>
  <thead>
    <tr>
      <th>
        FEATURE GUIDE
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
        Feature introduced in
      </td>
      
      <td>
        FRINX 2.3.0
      </td>
      
      <td>
        CLI service module with support for structured and unstructured data exchange
      </td>
    </tr>
    
    <tr>
      <td>
      </td>
      
      <td>
      </td>
      
      <td>
        CLI plugin:
      </td>
    </tr>
    
    <tr>
      <td>
        Feature introduced in
      </td>
      
      <td>
        FRINX 2.3.1
      </td>
      
      <td>
        Keepalive settings of CLI connection extracted into CLI node configuration
      </td>
    </tr>
    
    <tr>
      <td>
        Feature introduced in
      </td>
      
      <td>
        FRINX 2.3.1
      </td>
      
      <td>
        Translate registry additional information: Actual YANG model nodes that are supported/implemented are listed for each YANG model
      </td>
    </tr>
    
    <tr>
      <td>
        Feature introduced in
      </td>
      
      <td>
        FRINX 2.3.1
      </td>
      
      <td>
        Dry-run and journaling capabilities for CLI mountpoint: Enables users to write/read configuration to/from device as a dry-run operation to check what commands will ODL execute. Journal captures all executed commands for a CLI mountpoint and makes them visible for users.
      </td>
    </tr>
    
    <tr>
      <td>
      </td>
      
      <td>
      </td>
      
      <td>
        IOS support:
      </td>
    </tr>
    
    <tr>
      <td>
        Feature introduced in
      </td>
      
      <td>
        FRINX 2.3.1
      </td>
      
      <td>
        Openconfig interface YANG models support: Interface Configuration and State read/write support
      </td>
    </tr>
    
    <tr>
      <td>
        Feature introduced in
      </td>
      
      <td>
        FRINX 2.3.1
      </td>
      
      <td>
        Openconfig interface YANG models support: Interface Ipv4 read/write support
      </td>
    </tr>
    
    <tr>
      <td>
        Feature introduced in
      </td>
      
      <td>
        FRINX 2.3.1
      </td>
      
      <td>
        Openconfig BGP & RIB YANG models read support
      </td>
    </tr>
    
    <tr>
      <td>
        Feature introduced in
      </td>
      
      <td>
        FRINX 2.3.1
      </td>
      
      <td>
        Initial custom interface YANG model removed
      </td>
    </tr>
  </tbody>
</table>

 [1]: https://github.com/FRINXio/postman-collections
 [2]: https://www.getpostman.com/postman
 [3]: https://frinx.io/wp-content/uploads/2017/08/cliSouthPlugin5.png "CLI southbound plugin"
 [4]: https://frinx.io/wp-content/uploads/2017/08/cliMountpoint2.png "CLI mountpoint"
 [5]: https://frinx.io/wp-content/uploads/2017/06/iosUnits.png "IOS translation plugin"
 [6]: https://frinx.io/wp-content/uploads/2017/08/readCfg2.png "Config data"
 [7]: https://frinx.io/wp-content/uploads/2017/08/readOper2.png "Operational data"
 [8]: https://frinx.io/frinx-documents/running-frinx-odl-distribution-for-the-first-time.html
 [9]: https://frinx.io/wp-content/uploads/2017/06/mount-telnet.jpg
 [10]: https://frinx.io/wp-content/uploads/2017/06/mount-ssh.jpg
 [11]: https://frinx.io/frinx-documents/cli-service-module-devguide.html
 [12]: https://frinx.io/frinx-feature-guide/frinx-cli-supported-devices.html
 [13]: http://46.229.232.136:8888/