---
ID: 752
post_title: Running after activation
author: frinxeditor
post_date: 2016-06-01 14:40:57
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/running-frinx-odl-distribution-after-activation.html
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

Once a local license file has been generated you can start karaf without providing a token.

Using the command line, navigate to the folder that was just extracted. Now run

    bin/karaf clean
    

The clean parameter is optional and clears the karaf cache. When restarting the controller, using this option will delete features you previously installed. This is useful when recovering the controller to a known state.

You should see a karaf prompt similar to this one:

      ./bin/karaf clean
           _________      .__                  
           __________ __|__| ____ __  ___    
             / | ___  V__  |/      /  /    
            /  |  |   |  |  |   |          
            __| / |___|  |__>___|  /_/__   
               /                 /           
    Frinx version: 1.0.0-Beryllium-SR1.2-frinx frinx-user@root>
    

Once the controller is started press `Tab` to see the CLI commands available. [/wpmem_form]