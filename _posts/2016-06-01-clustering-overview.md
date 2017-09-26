---
ID: 768
post_title: Clustering
author: frinxeditor
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/clustering-overview.html
published: true
post_date: 2016-06-01 08:17:31
---
Clustering is a mechanism that enables multiple processes and programs to work together as one entity. For example, a Google Web search is in fact processed by thousands of web servers connected in a cluster. Similarly, you can have multiple instances of the OpenDaylight controller working together as one entity. There are a number of uses for clustering:

**Scaling**  
If you have multiple controllers running, you can potentially do more work with or store more data on those controllers if they are clustered. You can also break your data into smaller chunks (known as shards) and either distribute that data across the cluster or perform certain operations on certain members of the cluster.

**High Availability**  
If you have multiple controllers running and one crashes, you would still have the other instances working and available.

**Data Persistence**  
You will not lose any data gathered by your controller after a manual restart or a crash. The following sections describe how to set up clustering on both individual and multiple OpenDaylight controllers.

**Single Node Clustering**  
To enable clustering on a single OpenDaylight controller:  
1\. Navigate to the /bin directory.  
2\. Run Karaf:

    ./karaf  
    

3\. Install the clustering feature:

    feature:install odl-mdsal-clustering   
    

4\. If you are using the integration distribution of Karaf, you should also install the open flow plugin flow services:

    feature:install odl-openflowplugin-flow-services  
    

5\. Install the Jolokia bundle:

    bundle.install -s mvn:org.jolokia/jolokia-osgi/1.1.5  
    

After enabling the DistributedDataStore feature in a single instance, you can access the following features:

**Data Sharding**:  
The in-memory MD-SAL tree is broken up into a number of smaller sub-trees (inventory, topology, and default).

**Data Persistence**:  
All of the data available on defined data shards is stored on a disk. By restarting the controller, you can use the persisted data to reinstate those shards to their previous state.

**Multiple Node Clustering**  
**a. Deployment Considerations**  
We recommend a minimum of three machines. You can set up a cluster with just two nodes, however if one goes down, the controller will no longer be operational. Every device that belongs to a cluster needs an identifier. For this purpose, OpenDaylight uses the node’s role. After you define the first node’s role as member-1 in the akka.conf file, OpenDaylight uses member-1 to identify that node. Data shards are used to house all or a certain segment of a module’s data. For example, one shard can contain all of a module’s inventory data while another shard contains all of its topology data.

If you do not specify a module in the modules.conf file and do not specify a shard in module-shards.conf, then (by default) all the data is placed onto the default shard (which must also be defined in module-shards.conf file). Each shard has replicas configured, which can be specified in the module-shards.conf file. If you have a three node cluster on which HA is enabled, a replica of every defined data shard must be running on all three cluster nodes. This is because OpenDaylight’s clustering implementation requires a majority of the defined shard replicas to be running in order to function. If you only define data shard replicas on two of the cluster nodes and one of those goes down, the corresponding data shards will not function. If you have a three node cluster and have defined replicas for a data shard on each of those nodes, that shard will still function even if only two of the cluster nodes are running. Note that if one of those two nodes go down, your controller will no longer be operational.

*What considerations need to be made when setting the seed nodes for each member?*  
*Why are we referring to multiple seed nodes when you set only one IP address?*  
*Can you set multiple seed nodes for functional testing?*

We recommend that you have multiple seed nodes configured. After a cluster member is started, it sends a message to all of its seed nodes. The cluster member then sends a join command to the first seed node that responds. If none of its seed nodes reply, the cluster member repeats this process until it successfully establishes a connection or it is shutdown.

*What happens after one node becomes unreachable? Do the other two nodes function normally?* *When the first node reconnects, does it automatically synchronize with the other nodes?*

After a node becomes unreachable, it remains down for a configurable period of time (10 seconds by default). Once a node goes down, you need to restart it so that it can rejoin the cluster. Once a restarted node joins a cluster, it will synchronize with the lead node automatically. You can run a two node cluster for functional testing, but for HA testing you need to run all three nodes.

**b. Setting Up a Multiple Node Cluster**  
To run an OpenDaylight controller in a three node cluster, do the following:  
1\. Determine the three machines that will make up the cluster and copy the controller distribution to each of those machines.  
2\. Unzip the controller distribution.  
3\. Navigate to the /bin directory.  
4\. Run Karaf:

    ./karaf  
    

5\. Install the clustering feature:

    feature:install odl-mdsal-clustering  
    

Note: To run clustering, you must install the odl-mdsal-clustering feature on each of your nodes.  
6\. If you are using the integration distribution of Karaf, you should also install the open flow plugin flow services:

    feature:install odl-openflowplugin-flow-services  
    

7\. Install the Jolokia bundle:

    bundle.install -s mvn:org.jolokia/jolokia-osgi/1.1.5  
    

8\. On each node, open the following .conf files: 'configuration/initial/akka.conf' 'configuration/initial/module-shards.conf' In each configuration file, make the following changes:

Find every instance of the following lines and replace *127\.0.0.1* with the hostname or IP address of the machine on which the controller will run:

    netty.tcp {hostname = "127.0.0.1"}`
    

The value you need to specify will be different for each node in the cluster.

Find the following lines and replace *127\.0.0.1* with the hostname or IP address of any of the machines that will be part of the cluster:

    cluster {seed-nodes = ["akka.tcp://opendaylight-cluster-data@127.0.0.1:2550"]}
    

Find the following section and specify the role for each member node. For example, you could assign the first node with the *member-1* role, the second node with the *member-2* role, and the third node with the *member-3* role. roles = ["member-1"] Open the `configuration/initial/module-shards.conf` file and update the items listed in the following section so that the replicas match roles defined in this host’s akka.conf file.

    replicas = ["member-1"]
    

For reference, view a sample akka.conf file here: <https://gist.github.com/moizr/88f4bd4ac2b03cfa45f0>

Run the following commands on each of your cluster’s nodes:

    JAVA_MAX_MEM=4G JAVA_MAX_PERM_MEM=512m  
    ./karaf JAVA_MAX_MEM=4G JAVA_MAX_PERM_MEM=512m  
    ./karaf JAVA_MAX_MEM=4G JAVA_MAX_PERM_MEM=512m  
    ./karaf
    

The OpenDaylight controller can now run in a three node cluster. Use any of the three member nodes to access the data residing in the datastore. Say you want to view information about shard designated as *member-1* on a node. To do so, query the shard’s data by making the following HTTP request: *HTTP Method: GET* *HTTP URL:* <http://localhost:8181/jolokia/read/org.opendaylight.controller:Category=Shards,name=member-1-shard-inventory-config,type=DistributedConfigDatastore>

If prompted, enter admin as both the username and password.  
*HTTP: EXPECTED RESPONSE*  
This request should return the following information:  
{ "timestamp": 1410524741, "status": 200, "request": { "mbean": "org.opendaylight.controller:Category=Shards,name=member-1-shard-inventory-config,type=DistributedConfigDatastore", "type": "read" }, "value": { "ReadWriteTransactionCount": 0, "LastLogIndex": -1, "MaxNotificationMgrListenerQueueSize": 1000, "ReadOnlyTransactionCount": 0, "LastLogTerm": -1, "CommitIndex": -1, "CurrentTerm": 1, "FailedReadTransactionsCount": 0, "Leader": "member-1-shard-inventory-config", "ShardName": "member-1-shard-inventory-config", "DataStoreExecutorStats": { "activeThreadCount": 0, "largestQueueSize": 0, "currentThreadPoolSize": 1, "maxThreadPoolSize": 1, "totalTaskCount": 1, "largestThreadPoolSize": 1, "currentQueueSize": 0, "completedTaskCount": 1, "rejectedTaskCount": 0, "maxQueueSize": 5000 }, "FailedTransactionsCount": 0, "CommittedTransactionsCount": 0, "NotificationMgrExecutorStats": { "activeThreadCount": 0, "largestQueueSize": 0, "currentThreadPoolSize": 0, "maxThreadPoolSize": 20, "totalTaskCount": 0, "largestThreadPoolSize": 0, "currentQueueSize": 0, "completedTaskCount": 0, "rejectedTaskCount": 0, "maxQueueSize": 1000 }, "LastApplied": -1, "AbortTransactionsCount": 0, "WriteOnlyTransactionCount": 0, "LastCommittedTransactionTime": "1969-12-31 16:00:00.000", "RaftState": "Leader", "CurrentNotificationMgrListenerQueueStats": [] } }

The key thing here is the name of the shard. Shard names are structured as follows:

    <member-name>-shard-<shard-name-as-per-configuration>-<store-type>  
    

Here are a couple of sample data short names: • member-1-shard-topology-config • member-2-shard-default-operational Content of this section provided from under *Apache 2.0 license* from [https://nexus.opendaylight.org/content/sites/site/org.opendaylight.docs/master/userguide/manuals/userguide/bk-user-guide/content/\_setting\_up_clustering_on_an_opendaylight_controller.html ][1]

**c. Deploying a cluster automatically**  
The cluster can be also deployed automatically using a script developed by the OpenDaylight integration project. The script is available from their Git repository.

    git clone
    

https://git.opendaylight.org/gerrit/integration/test.git

    cd test/tools/clustering/cluster-deployer/ 
    

Instructions for use are available at:

<https://wiki.opendaylight.org/view/Running_and_testing_an_OpenDaylight_Cluster>

 [1]: https://nexus.opendaylight.org/content/sites/site/org.opendaylight.docs/master/userguide/manuals/userguide/bk-user-guide/content/_setting_up_clustering_on_an_opendaylight_controller.html