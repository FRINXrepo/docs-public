---
ID: 4750
post_title: 'Protected: CLI Plugin user guide'
author: frinxadmin
post_date: 2017-06-21 10:46:36
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/cli-user-guide.html
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
The CLI southbound plugin for Opendaylight enables the controller to manage devices over a CLI. Much like the netconf southbound plugin, it enables fully model-driven, transactional device management for internal and external OpenDaylight applications. In fact, the applications are completely unaware of underyling transport and can manage devices over the CLI in the same exact way as devices over netconf.

![CLI southbound plugin][1]

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

![CLI mountpoint][2]

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

![IOS translation plugin][3]

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

![Config data][4]

*   **Operational** 
    *   actual configuration on the device
    *   optionally statistics from the device
    *   translation plugins/units need to pull these data out of the device when R(ead) operation is requested

![Operational data][5]

*   **RPCs** stand on their own and can actually encapsulate any command(s) on the device.

### Transactions and revert

As mentioned before, configuring a device is performed within transactions. If it's impossible to perform device configuration, the user/app facing transaction is failed and a revert procedure is initiated (in case there was partial configuration already submitted to the device).

### Reconciliation

There might be situations where there are inconsistencies between actual configuration on the device and the state cached in Opendaylight. That's why a reconciliation mechanism was developed to:

*   Allow the mountpoint to sync its state when first connecting to the device
*   Allow apps/users to request synchronization when an inconsistent state is expected e.g. manual configuration of the device

## Mounting a CLI device

The following sequence of operations needs to happen from the point when Opendaylight is configured to mount a CLI device until it is truly accessible for users and applications:

1.  Submit CLI device configuration into CLI topology 
    *   Over REST, NETCONF or from within Opendaylight
2.  CLI topology opens transport layer by opening a session with the device
3.  CLI topology collects all the units into a plugin and instantiates translation layer
4.  CLI topology builds mountpoint services on top of the translation layer
5.  CLI topology exposes the mountpoint into MD-SAL
6.  CLI topology updates operational state of this node in CLI topology to connected

## Usage

This section provides samples for how to use the CLI southbound plugin to manage a particular device.

### Features

Install the following features into a running FRINX OpenDaylight instance:

    feature:install cli-topology cli-southbound-unit-generic cli-southbound-unit-ios-essential 
    odl-restconf
    

This installs the CLI topology, a baseline translation unit and an IOS essential unit.

### Logs

If finer logging is required, use the following command to enable DEBUG/TRACE logging:

    log:set TRACE io.frinx.cli
    

### Listing supported devices over REST

It is possible to check a current list of units and thus a current list of supported devices directly from OpenDaylight's REST interface. Please refer to [POSTMAN collection][6], folder *CLI registry* to see the actual list:

### IOS device

#### Mounting and managing over REST

Please refer to the [POSTMAN collection][6], folder *Ios mount*:

#### Mounting and managing from an application

It is also possible to manage an IOS device in a similar fashion from within an OpenDaylight application. It is however necessary to acquire an appropriate mountpoint instance from MD-SAL's mountpoint service.

To do so, first make sure to generate an appropriate Opendaylight application using the archetype.

Next make sure to add a Mountpoint service as a dependency of the application, so update your blueprint:

    <reference id="mountpointService"
               interface="org.opendaylight.mdsal.binding.api.MountPointService"/>
    

and add an argument to your component:

    <bean id="SOMEBEAN"
      class="PACKAGE.SOMEBEAN"
      init-method="init" destroy-method="close">
      <argument ref="dataBroker" />
      ...
      <argument ref="mountpointService"/>
    </bean>
    

Also add that argument to your constructor:

      final MountPointService mountpointService
    

So now to get a connected mountpoint from the service:

    Optional [MountPoint] mountPoint = a.getMountPoint(InstanceIdentifier.create(NetworkTopology.class) .child(Topology.class, new TopologyKey(new TopologyId("cli"))) .child(Node.class, new NodeKey(new NodeId("IOS1"))));
    
    if(mountPoint.isPresent()) { // Get DATA broker Optional<DataBroker> dataBroker = mountPoint.get().getService(DataBroker.class); // Get RPC service Optional<RpcService> rpcService = mountPoint.get().getService(RpcService.class);
    
        if(!dataBroker.isPresent()) {
            // This cannot happen with CLI mountpoints
            throw new IllegalArgumentException("Data broker not present");
        }
    
    
    }
    

And finally DataBroker service can be used to manage the device:

    ReadWriteTransaction readWriteTransaction = dataBroker.get().newReadWriteTransaction(); // Perform read // reading operational data straight from device CheckedFuture<Optional<Version>, ReadFailedException> read = readWriteTransaction.read(LogicalDatastoreType.OPERATIONAL, InstanceIdentifier.create(Version.class)); try { Version version = read.get().get(); } catch (InterruptedException | ExecutionException e) { e.printStackTrace(); }
    
    Futures.addCallback(readWriteTransaction.submit(), new FutureCallback<Void>() { @Override public void onSuccess(@Nullable Void result) { // Successfully invoked TX }
    
        @Override
        public void onFailure(Throwable t) {
            // TX failure
        }
    
    
    }); 
    

In this case *Version* operational data is being read from the device. In order to be able to do so, make sure to add a maven dependency on the IOS unit containing the appropriate YANG model.

### Generic Linux VM

#### Mounting and managing over REST

Please refer to the [POSTMAN collection][6], folder *Linux mount*:

## Supported devices

This section lists all the device types currently supported by the CLI southbound plugin and configuration aspects implemented for them.

### IOS

IOS device management is supported. Currently supported aspects:

*   interface management 
*   VRF management 
*   Version data read 

### Generic device

It is possible to mount any network device as a generic device. This allows invocation of any commands on the device using RPCs, which return the output back as freeform data and it is up to user/application to make sense of them.

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
        CLI service module with support for structured and unstructured data exchange
      </td>
    </tr>
  </tbody>
</table>

 [1]: https://frinx.io/wp-content/uploads/2017/06/cliSouthPlugin.png "CLI southbound plugin"
 [2]: https://frinx.io/wp-content/uploads/2017/06/cliMountpoint.png "CLI mountpoint"
 [3]: https://frinx.io/wp-content/uploads/2017/06/iosUnits.png "IOS translation plugin"
 [4]: https://frinx.io/wp-content/uploads/2017/06/readCfg.png "Config data"
 [5]: https://frinx.io/wp-content/uploads/2017/06/readOper.png "Operational data"
 [6]: https://frinx.io/uncategorized/postman-json.html