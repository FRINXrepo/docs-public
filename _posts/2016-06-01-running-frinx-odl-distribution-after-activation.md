---
ID: 752
post_title: >
  Running the FRINX ODL Distribution after
  activation
author: frinxeditor
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/running-frinx-odl-distribution-after-activation.html
published: true
post_date: 2016-06-01 14:40:57
---
After running for the first time and generating a local license file, you no longer need to provide a token when starting karaf.

To start karaf, go to your Frinx ODL Distribution folder, for example /home/username/distribution-karaf-2.3.0.frinx.

Then type

    bin/karaf 
    

If you want to start the controller cleanly - that is, deleting any features you previously installed - then you can instead use

    /bin/karaf clean
    

The clean parameter clears the karaf cache. This is useful when recovering the controller to a known state.

After starting karaf you should see a karaf prompt similar to this one:

      /bin/karaf clean
           _________      .__                  
           __________ __|__| ____ __  ___    
             / | ___  V__  |/      /  /    
            /  |  |   |  |  |   |          
            __| / |___|  |__>___|  /_/__   
               /                 /           
    Frinx version: 1.0.0-Beryllium-SR1.2-frinx frinx-user@root>
    

Once the controller is started press `Tab` to see the CLI commands available.