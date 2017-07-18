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
See our Elasticsearch video [here][1]

**Prerequisites**  
1\. [Install the FRINX ODL distribution][2]  
2\. Install Logstash, ElasticSearch and Kibana. The easiest way is to pull a pre-configured Docker image which includes all three. We have used [this one][3] and recommend it. If you use this method you can ignore prerequisites 3,4 and 5 below.

3\. [Install Logstash][4] - Collecting and parsing log files. It can transform an unstructured log into something meaningful and searchable.  
4\. [Install Elasticsearch][5] - Store the data that Logstash processed and provide a full-text index  
5\. Kibana (optional) - Web console allowing the user to interact with Elasticsearch. Kibana can be [downloaded][6] or pulled as a Docker image - several exist.

The base configuration is to use log4j socket listener for Logstash and the log4j socket appender in ODL Frinx.

**Configure Log4j**

In the Frinx ODL distribution, go to your /etc directory.

Backup your old Log4j config if it exists:

    mv org.ops4j.pax.logging.cfg org.ops4j.pax.logging.cfg.bkp
    

Create a new config file using the following command

    cat << EOF > org.ops4j.pax.logging.cfg
    

This will change the first four lines of the config file:

    log4j.rootLogger= INFO, out,ELKTransform,osgi:* log4j.appender.ELKTransform=org.apache.log4j.net.SocketAppender log4j.appender.ELKTransform.port=9500  log4j.appender.ELKTransform.remoteHost=127.0.0.1 log4j.throwableRenderer=org.apache.log4j.OsgiThrowableRenderer
    
    # CONSOLE appender not used by default  
    log4j.appender.stdout=org.apache.log4j.ConsoleAppender log4j.appender.stdout.layout=org.apache.log4j.PatternLayout log4j.appender.stdout.layout.ConversionPattern=%d{ISO8601} | %-5.5p | %-16.16t | %-32.32c{1} | %X{bundle.id} - %X{bundle.name} - %X{bundle.version} | %m%n
    
    # Async appender forwarding to file appender  
    log4j.appender.async=org.apache.log4j.AsyncAppender log4j.appender.async.appenders=out
    
    # File appender  
    log4j.appender.out=org.apache.log4j.RollingFileAppender log4j.appender.out.layout=org.apache.log4j.PatternLayout log4j.appender.out.layout.ConversionPattern=%d{ISO8601} | %-5.5p | %-16.16t | %-32.32c{1} | %X{bundle.id} - %X{bundle.name} - %X{bundle.version} | %m%n log4j.appender.out.file=${karaf.data}/log/karaf.log log4j.appender.out.append=true log4j.appender.out.maxFileSize=1MB log4j.appender.out.maxBackupIndex=10
    
    # Sift appender  
    log4j.appender.sift=org.apache.log4j.sift.MDCSiftingAppender log4j.appender.sift.key=bundle.name log4j.appender.sift.default=karaf log4j.appender.sift.appender=org.apache.log4j.FileAppender log4j.appender.sift.appender.layout=org.apache.log4j.PatternLayout log4j.appender.sift.appender.layout.ConversionPattern=%d{ISO8601} | %-5.5p | %-16.16t | %-32.32c{1} | %m%n log4j.appender.sift.appender.file=${karaf.data}/log/${bundle.name}.log log4j.appender.sift.appender.append=true EOF \``\`  
    

**Configure Logstash**

We must configure socket lister for Logstash by creating a file named logstash.conf in the logstash directory. Create the file, and enter the following into it. Paramters in [] are explained below:

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

For more info see: [Getting started with Logstash][7] and [Log4j][8]

**Run ODL**

Start a karaf session: `KARAF_HOME/bin/karaf` All information is logged to an Elasticsearch node though Logstash where you can define for example pipelines.

Kibana can be downloaded locally or as a Docker image (several exist). [Configuring Kibana][9]

**Other links**  
[Elastic search products][10]  
[Installing Logstash][11]  
[Running Logstash and Elasticsearch in docker][12]  
[How To Install Elasticsearch, Logstash, and Kibana (ELK Stack) on Ubuntu 14.04][13]

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
 [3]: http://elk-docker.readthedocs.io/#elasticsearch-logstash-kibana-elk-docker-image-documentation
 [4]: https://www.elastic.co/guide/en/logstash/current/installing-logstash.html
 [5]: https://www.elastic.co/downloads/elasticsearch
 [6]: https://www.elastic.co/downloads/kibana
 [7]: https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html "Getting started with Logstash"
 [8]: https://www.elastic.co/guide/en/logstash/current/plugins-inputs-log4j.html "Log4j"
 [9]: https://www.elastic.co/guide/en/kibana/current/index.html "Configuring KIbana"
 [10]: https://www.elastic.co/products "Elastic search products"
 [11]: https://www.elastic.co/guide/en/logstash/current/installing-logstash.html "Installing Logstash"
 [12]: https://www.elastic.co/guide/en/logstash/current/docker.html "Running Logstash and Elastic Search in Docker"
 [13]: https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elk-stack-on-ubuntu-14-04 "How To Install Elasticsearch, Logstash, and Kibana (ELK Stack) on Ubuntu 14.04"