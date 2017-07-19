---
ID: 3404
post_title: Elastic Search
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/elastic-search.html
published: true
post_date: 2017-01-03 08:19:00
---
For an introduction, see our Elasticsearch video [here][1]

1\. If you have not already done so, [Install the FRINX ODL distribution][2]  
2\. [Install logstash][3] which we'll use for collecting and parsing log files. It can transform an unstructured log into something meaningful and searchable. 3. [Install Elasticsearch][4] - Store the data that Logstash processed and provide a full-text index  
4\. Kibana (optional) - Web console allowing the user to interact with Elasticsearch. Kibana can be [downloaded][5] or pulled as a Docker image - several exist.

The base configuration is to use log4j socket listener for Logstash and the log4j socket appender in ODL Frinx.

**Configure Log4j**

In the Frinx ODL distribution, go to your /etc directory.

Backup your old Log4j config if it exists:

    mv org.ops4j.pax.logging.cfg org.ops4j.pax.logging.cfg.bkp
    

Now open org.ops4j.pax.logging.cfg in a text editor.

At the top of the file, under 'Root logger' you will see the following lines:

> log4j.rootLogger=INFO, async, osgi:*
> 
> log4j.category.org.apache.karaf.features=DEBUG log4j.category.io.frinx=DEBUG log4j.category.org.opendaylight.controller.cluster=DEBUG log4j.category.org.opendaylight.netconf.sal.connect=DEBUG log4j.category.org.opendaylight.netconf.topology=DEBUG

Replace the first four of these lines with the following:

> log4j.rootLogger= INFO, out,ELKTransform,osgi:*
> 
> log4j.appender.ELKTransform=org.apache.log4j.net.SocketAppender log4j.appender.ELKTransform.port=9500 log4j.appender.ELKTransform.remoteHost=127.0.0.1

Save the file.

**Configure Logstash**

We must now configure socket listener for Logstash by creating a file named logstash.conf in the logstash directory, which was created automatically when you started the Docker container. Create the file, and enter the following into it. Parameters in [] are explained below:

    input {
      log4j {
        mode => server
        port => [logstash_port]
        type => "log4j"
      }
    }
    output {
      elasticsearch {
        protocol => "http"
        host => "[elk_host]"
        port => "[elk_port]"
      }
    }
    

Set the **logstash port** to **9500**. The **elk_host** and **elk_port** depend on how and where Elasticsearch is installed - by default **Logstash** and **Elasticsearch** are on the same server. So for example host is **127\.0.0.1** and the port is the default **9200**.

For more info see: [Getting started with Logstash][6] and [Log4j][7]

**Run the FRINX ODL Distribution**

Start karaf as normal by first opening a terminal and going to your FRINX ODL Distribution main directory for example distribution-karaf-2.3.0.frinx.

Start karaf with the command

    bin/karaf
    

All logging information is now logged to an Elasticsearch node though Logstash. This information can be analysed with Kibana.

**Other links**  
[Elastic search products][8]  
[Installing Logstash][9]  
[Running Logstash and Elasticsearch in docker][10]  
[How To Install Elasticsearch, Logstash, and Kibana (ELK Stack) on Ubuntu 14.04][11]

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
        FRINX 1.4.0
      </td>
      
      <td>
        Elastic search module
      </td>
    </tr>
  </tbody>
</table>

 [1]: https://youtu.be/_nIIiZSh0Qs
 [2]: https://frinx.io//downloads/ "FRINX distribution"
 [3]: https://www.elastic.co/downloads/logstash
 [4]: https://www.elastic.co/downloads/elasticsearch
 [5]: https://www.elastic.co/downloads/kibana
 [6]: https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html "Getting started with Logstash"
 [7]: https://www.elastic.co/guide/en/logstash/current/plugins-inputs-log4j.html "Log4j"
 [8]: https://www.elastic.co/products "Elastic search products"
 [9]: https://www.elastic.co/guide/en/logstash/current/installing-logstash.html "Installing Logstash"
 [10]: https://www.elastic.co/guide/en/logstash/current/docker.html "Running Logstash and Elastic Search in Docker"
 [11]: https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elk-stack-on-ubuntu-14-04 "How To Install Elasticsearch, Logstash, and Kibana (ELK Stack) on Ubuntu 14.04"