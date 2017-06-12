---
ID: 755
post_title: 'Enable Feature Manager &#038; System Manager'
author: frinxeditor
post_date: 2016-06-01 14:41:40
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/enabling-feature-manager-system-manager-in-karaf.html
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
[wpmem_form login]  
**Enabling Feature Manager (installer) frontend**  
Currently this feature is installed automatically. You can confirm this by typing the following text in the karaf console:

    frinx-user@root> feature:list -i | grep frinx-installer-gui 
    

If there is no output, install it manually:

    frinx-user@root> feature:install frinx-installer-gui  
    

Open this link in a browser: <http://localhost:8181/index.html>

(Username admin, password admin).  
You should see a link 'Feature Manager'.

**Enabling System Manager frontend – BETA**  
This feature is in BETA release state, it is installed automatically but uses separate authentication to the Feature Manager. To install manually, type:

    frinx-user@root> feature:install frinx-config-gui Open this link in a browser:  
    

<http://localhost:8181/index.html#/configmgr/index>  

(Username karaf, password karaf) [/wpmem_form]