---
ID: 3404
post_title: Elastic Search
author: frinxadmin
post_date: 2017-01-03 08:19:00
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/elastic-search.html
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
See our Elasticsearch video [here][1]

**Prerequisites**  
1\. [FRINX distribution][2]  
2\. Logstash - Collecting and parsing log files. It can transform an unstructured log into something meaningful and searchable  
3\. Elasticsearch - Store the data that Logstash processed and provide a full-text index  
4\. Kibana (optional) - Web console allowing the user to interact with Elasticsearch.

The base configuration is to use log4j socket listener for Logstash and the log4j socket appender in ODL Frinx.

**Configure Log4j**

In the Frinx ODL distribution, go to your `KARAF_HOME/etc` directory.

Backup your old config if it exists:

    mv org.ops4j.pax.logging.cfg org.ops4j.pax.logging.cfg.bkp
    

Create a new config file using the following command (this will change the first four lines of the config file):

    cat << EOF > org.ops4j.pax.logging.cfg
    
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
    

The **elk_host** and **elk_port** depend on how and where Elasticsearch is installed - by default Logstash and Elasticsearch are on the same server. So for example host is 127.0.0.1 and the port is the default 9200.

For more info see: [Getting started with Logstash][3] and [Log4j][4]

**Run ODL**

Start a karaf session: `KARAF_HOME/bin/karaf` All information is logged to an Elasticsearch node though Logstash where you can define for example pipelines.

Kibana can be downloaded locally or as a Docker image (several exist). [Configuring Kibana][5]

**Other links**  
[Elastic search products][6]  
[Installing Logstash][7]  
[Running Logstash and Elasticsearch in docker][8]  
[How To Install Elasticsearch, Logstash, and Kibana (ELK Stack) on Ubuntu 14.04][9]

<img src="https://frinx.io/wp-content/uploads/2017/01/feat-es.png" alt="" width="629" height="94" class="alignleft size-full wp-image-4881" />

 [1]: https://youtu.be/_nIIiZSh0Qs
 [2]: https://frinx.io//downloads/ "FRINX distribution"
 [3]: https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html "Getting started with Logstash"
 [4]: https://www.elastic.co/guide/en/logstash/current/plugins-inputs-log4j.html "Log4j"
 [5]: https://www.elastic.co/guide/en/kibana/current/index.html "Configuring KIbana"
 [6]: https://www.elastic.co/products "Elastic search products"
 [7]: https://www.elastic.co/guide/en/logstash/current/installing-logstash.html "Installing Logstash"
 [8]: https://www.elastic.co/guide/en/logstash/current/docker.html "Running Logstash and Elastic Search in Docker"
 [9]: https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elk-stack-on-ubuntu-14-04 "How To Install Elasticsearch, Logstash, and Kibana (ELK Stack) on Ubuntu 14.04"