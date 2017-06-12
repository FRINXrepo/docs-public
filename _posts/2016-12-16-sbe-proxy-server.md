---
ID: 3342
post_title: Proxy server
author: frinxadmin
post_date: 2016-12-16 12:06:51
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/sbe-proxy-server.html
published: true
sidebar:
  - ""
footer:
  - ""
header_title_bar:
  - ""
header_transparency:
  - ""
apost_date:
  - 'a:1:{i:0;s:19:"2016-11-16 12:51:40";}'
hheader_title_bar:
  - 'a:1:{i:0;s:17:"a:1:{i:0;s:0:"";}";}'
---
[wpmem_form login]

### Proxy server configuration

This part describe how to setup SBE proxy server, if you provide more SBE instances on more hosts. SBE proxy server is reverse proxy server provided by NGINX.

**Figure 1: Multi host provision**  
![Figure1: Multi host providing][1]

**Proxy settings**

All proxy rules and options are defined in the **sbe.proxy** file in sbe project root.

    PROXY_HOST="localhost" -> Host or FQDN where is proxy provided PROXY_PORT=80 -> Port where is proxy listen
    
    PROXY_RULES_WEB=(
    
            "redmine.localhost=http://redmine.host1/"       -> **Transport rule for HTTP**
            "gerrit.localhost=http://gerrit.host1/"
            "jenkins.localhost=http://jenkins.host1/"
            "nexus.localhost=http://nexus.host1/"
    
            "redmine.titan.localhost=http://redmine.host2/"
            "gerrit.titan.localhost=http://gerrit.host2/"
            "jenkins.titan.localhost=http://jenkins.host2/"
            "nexus.titan.localhost=http://nexus.host2/"
    
    
    )
    
        PROXY_RULES_SSH=(
    
            "git.localhost:29418=host1:29418"           -> **Transport rule for SSH**
            "git.titan.localhost:29418=host2:29418"
    
    
    )
    

**Proxy control**

Start proxy server

    ./sbe proxy-start
    

Stop proxy server

    ./sbe proxy-stop
    

Restart proxy server

    ./sbe proxy-restart
    

[/wpmem_form]

 [1]: https://gerrit.frinx.io/plugins/gitblit/raw/sbe-doc.git/master/3-multi-host.png