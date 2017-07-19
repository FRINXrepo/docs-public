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

## Installation

1\. If you have not already done so, [Download the FRINX ODL distribution][2] and [install it][3]  
2\. [Install Elasticsearch][4] - download the zip file, then unpackage it by opening a terminal, going to the directory where the download file is, and typing

    unzip filename
    

In the unpackaged folder, start elasticsearch with

    bin/elasticsearch
    

3\. [Install Kibana][5] - download the version appropriate to your system. For the Linuz-64 bit tar.gz download file, unpackage it with

    tar -xvf filename
    

In the unpackaged folder, start kibana with

    bin/kibana
    

4\. [Install logstash][6] - which we'll use for collecting and parsing log files. It can transform an unstructured log into something meaningful and searchable.

For the Linuz-64 bit tar.gz download file, unpackage it with

    tar -xvf filename
    

## Configuration

The base configuration is to use log4j socket listener for Logstash and the log4j socket appender in ODL Frinx.

**Configure Log4j**

In the Frinx ODL distribution, go to your /etc directory.

Backup your old Log4j config if it exists:

    cp org.ops4j.pax.logging.cfg org.ops4j.pax.logging.cfg.bkp
    

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

We must now configure socket listener for Logstash.

From your logstash folder (the folder created from unpackaging the download file at the start of this guide), move into the config folder:

    cd config
    

Create a blank file named logstash.conf

    touch frinx.conf
    

Enter the following into the file and save it. Parameters in [] are explained below:

    input {
      log4j {
        mode => server
        port => 9500
        type => "log4j"
      }
    }
    output {
      elasticsearch { hosts => ["localhost:9200"] }
    }
    

For more info see: [Getting started with Logstash][7] and [Log4j][8]

We started elasticsearch and kibana after downloading (see the start of this guide).

We now need to start logstash. Move to your main logstash folder:

    cd ..
    

The start logstash with

    bin/logstash -f config/frinx.conf
    

## Operation

We have already started elasticsearch, kibana, and logstash. Now start karaf as normal by going to your FRINX ODL Distribution main directory for example distribution-karaf-2.3.0.frinx.

Then type

    bin/karaf
    

All logging information is now logged to an Elasticsearch node though Logstash. This information can be analysed with Kibana. Open Kibana in a Web browser by going to <http://localhost:5601>

**Other links**  
[Elastic search products][9]  
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
 [3]: https://frinx.io/frinx-documents/running-frinx-odl-distribution-for-the-first-time.html
 [4]: https://www.elastic.co/downloads/elasticsearch
 [5]: https://www.elastic.co/downloads/kibana
 [6]: https://www.elastic.co/downloads/logstash
 [7]: https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html "Getting started with Logstash"
 [8]: https://www.elastic.co/guide/en/logstash/current/plugins-inputs-log4j.html "Log4j"
 [9]: https://www.elastic.co/products "Elastic search products"
 [10]: https://www.elastic.co/guide/en/logstash/current/docker.html "Running Logstash and Elastic Search in Docker"
 [11]: https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elk-stack-on-ubuntu-14-04 "How To Install Elasticsearch, Logstash, and Kibana (ELK Stack) on Ubuntu 14.04"