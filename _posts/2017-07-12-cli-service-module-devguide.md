---
ID: 4975
post_title: CLI Service Module Developer Guide
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/cli-service-module-devguide.html
published: true
post_date: 2017-07-12 10:32:45
---
This document provides developer-level details for the FRINX CLI southbound plugin, both for the framework itself as well as for the pluggable translation units.

Pre-requisite reading: - Honeycomb design documentation:  
<https://wiki.fd.io/view/Honeycomb>  
<https://docs.fd.io/honeycomb/1.17.04/release-notes-aggregator/release_notes.html>  
CLI plugin available presentations:  
<https://frinxhelpdesk.atlassian.net/wiki/display/~mmarsalek/CLI+southbound+plugin+docs> - CLI plugin user guide

## Building on honeycomb

The essential idea behind the CLI southbound plugin comes from Honeycomb. Honeycomb defines, implements and uses the same pipeline and the same framework to handle data. The APIs, some implementations and also SPIs used in the CLI southbound plugin's translation layer come from Honeycomb. However, the CLI southbound plugin creates multiple instances of Honeycomb components and encapsulates them behind a mount point.

The following series of diagrams shows the evolution from Opendaylight to Honeycomb and back into Opendaylight as a CLI mountpoint:

High level Opendaylight overview with its concept of a Mountpoint:

![ODL][1]

High level Honeycomb overview:

![HC][2]

Honeycomb core (custom MD-SAL implementation) overview:

![Honeycomb's core][3]

How Honeycomb is encapsulated as a mount point in Opendaylight:

![Honeycomb's core as mountpoint][4]

## Major components

The following diagram shows the major components of the CLI southbound plugin and their relationships: ![CLI plugin components][5]

## Modules

The following diagram shows project modules and their dependencies: ![CLI plugin modules][6]

## Developing a device specific translation unit

This section provides a tutorial for developing a device specific translation unit.

### Using the archetype

There is an archetype to generate a skeleton of a translation unit. To generate a skeleton from the archetype, invoke the following command:

    mvn -X archetype:generate -DarchetypeGroupId=io.frinx.cli -DarchetypeArtifactId=unit-archetype -DarchetypeVersion=0.1.0-SNAPSHOT
    

You will be asked to fill in some parameters. As an example, values could be:

    Define value for property 'device-type': ios
    [INFO] Using property: device-version = *
    Define value for property 'group-id-prefix': io.frinx.cli
    Define value for property 'unit-domain': vrfs
    Define value for property 'groupId' io.frinx.cli.ios.vrfs: :
    Define value for property 'artifactId' ios-vrfs-unit: :
    Define value for property 'version' 1.0-SNAPSHOT: :
    [INFO] Using property: version = 1.0-SNAPSHOT
    Define value for property 'package' io.frinx.cli.ios.vrfs: :
    [INFO] Using property: cli-version = 0.1.0-SNAPSHOT
    Define value for property 'unit-name' iosvrfsUnit: :
    

This will generate just a single maven module called *ios-vrfs-unit*. The module contains:

*   sample YANG model
*   2 handlers handling CRUD operations for a node inside the YANG model
*   glue code to inject itself into the CLI southbound plugin framework

Running maven build should now succeed for the new unit. From this point, the unit can be extended in any way necessary.

### Installing to Opendaylight

For a unit generated from the archetype, you can directly install it into the already running Opendaylight CLI southbound plugin. For how to run Opendaylight with the CLI southbound plugin, please refer to the [user guide][7]. To install a bundle with a new unit (e.g. previously built with maven) it is sufficient to run the following command in the karaf console:

    bundle:install -s file:///home/devel/ios-vrfs-unit/target/ios-vrfs-unit-1.0-SNAPSHOT.jar
    

Now the new unit should be reported by the CLI southbound plugin as being available. To verify its presence from RESTCONF, use the provided postman collection, *CLI registry* folder.

#### As a feature

It is also possible to include this bundle into a karaf feature and make it install with that particular feature instead of using the *bundle:install* command.

### Testing

Please see the end of this guide for how to mount a CLI device. If there is a new unit installed in Opendaylight, it will be possible to use the new unit's YANG model and its handlers.

### Choosing the right YANG models

Before writing a custom YANG model for a unit, it is important to check whether such a model doesn't already exist. There are plenty of YANG models available, modeling many aspects of network device management. The biggest groups of models are: - Openconfig https://github.com/openconfig/public/tree/master/release/models - IETF <https://github.com/YangModels/yang/tree/master/standard/ietf>

It is usually wiser to choose an existing YANG model instead of developing a custom one. Also it is very important to check for existing units already implemented for a device. If there are any, the best approach will most likely be to use YANG models from the same family as existing units use.

### Implementing handlers

There are 2 types of handlers. Those which handle writes of configuration data and those which handle reads of operational data. The responsibility of a handler is just to transform between CLI commands and the YANG data. There is nothing more a handler needs to do. For an example, refer to the section discussing unit archetype.

### Implementing RPCs

An RPC handler is a special kind of handler, different to the data handlers. RPC handler can encapsulate any commands. The biggest difference is that any configuration processing in RPCs is not part of transactions, reconciliation etc.

## Mounting a CLI device

The following sequence of operations needs to happen from the point when Opendaylight is configured to mount a CLI device until it is truly accessible for users and applications:

1.  Submit CLI device configuration into CLI topology 
    *   Over REST, NETCONF or from within Opendaylight
2.  CLI topology opens transport layer by opening a session with the device
3.  CLI topology collects all the units into a plugin and instantiates translation layer
4.  CLI topology builds mountpoint services on top of the translation layer
5.  CLI topology exposes the mountpoint into MD-SAL
6.  CLI topology updates operational state of this node in CLI topology to connected

### Mounting and managing Generic Linux VM over REST

Please refer to the [POSTMAN collection][1], folder *Linux mount*:

### Mounting and managing IOS devices over REST

Please refer to the [POSTMAN collection][1], folder *Ios mount*:

### Mounting and managing IOS devices from an application

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

 [1]: https://frinx.io/wp-content/uploads/2017/07/ODL.png "ODL"
 [2]: https://frinx.io/wp-content/uploads/2017/07/HC.png "HC"
 [3]: https://frinx.io/wp-content/uploads/2017/07/HCsMdsal.png "Honeycomb's core"
 [4]: https://frinx.io/wp-content/uploads/2017/07/cliMountpoint.png "Honeycomb's core as Mountpoint"
 [5]: https://frinx.io/wp-content/uploads/2017/07/cliInComponents.png "CLI plugin components"
 [6]: https://frinx.io/wp-content/uploads/2017/07/projectComponents.png "CLI plugin modules"
 [7]: https://frinx.io/frinx-documents/cli-service-module.html