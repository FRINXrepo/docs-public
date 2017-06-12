---
ID: 772
post_title: Karaf CLI
author: frinxeditor
post_date: 2016-06-01 14:45:50
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/using-the-frinx-odl-distribution-cli.html
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

The Apache Karaf container used by the Frinx ODL Distribution supports three different start modes:

1.  ***regular*** mode starts Apache Karaf in the foreground, including the shell console.
2.  ***server*** mode starts Apache Karaf in the foreground, without the shell console.
3.  ***background*** mode starts Apache Karaf in the background.

You can also manage Apache Karaf as a system service (see [System Service][1] section of this manual).

**Regular mode**  
Uses the `bin/karaf` Linux script (`binkaraf.bat` on Windows). It's the default start process. It starts Apache Karaf as a foreground process, and displays the shell console.

a. On Linux:

    ./bin/karaf
    
           _________      .__                  
           __________ __|__| ____ __  ___    
             / | ___  V__  |/      /  /    
            /  |  |   |  |  |   |          
            __| / |___|  |__>___|  /_/__   
               /                 /           
    Frinx version: 1.0.0-Beryllium-SR1.2-frinx frinx-user@root>
    Hit [tab] for a list of available commands and [cmd] --help</code> for help on a specific command.</pre>
    Hit `<ctrl-d>` or type `system:shutdown` or `logout` to shutdown Karaf.
    $karaf@root()>`
    

b. On Windows:

      binkaraf.bat
           _________      .__                  
           __________ __|__| ____ __  ___    
             / | ___  V__  |/      /  /    
            /  |  |   |  |  |   |          
            __| / |___|  |__>___|  /_/__   
               /                 /           
    Frinx version: 1.0.0-Beryllium-SR1.2-frinx frinx-user@root>
    
    Hit [tab] for a list of available commands
    

and `[cmd] --help` for help on a specific command.

Hit `<ctrl-d>` or type `system:shutdown` or `logout` to shutdown Karaf.

`karaf@root()>`

     Warning
     Closing the console or shell window will cause Apache Karaf and therefore Frinx to terminate.
    

**Server mode**  
Server mode starts Apache Karaf as a foreground process, but doesn't start the shell console. To use this mode, use the server argument to the `bin/karaf` Linux script (on Windows the script is at <span style="font-family: Courier New">binkaraf.bat</span>).  
a. On Linux:

    bin/karaf server
    

b. On Windows:

    binkaraf.bat server Warning  
    Closing the console or shell window will cause Apache Karaf to terminate.
    

You can connect to the shell console using SSH or client (see the Connect section in this page).

**Background mode**  
Background mode starts Apache Karaf as a background process. To start in background mode, you have to use the `bin/start` Linux script (`binstart.bat` on Windows).

a. On Linux:

    bin/start
    

b. On Windows:

    binstart.bat  
    You can connect to the shell console using SSH or client (see the Connect section).
    

**Clean start**  
Apache Karaf stores all previously installed applications and changes that you made in the data folder. If you want to start from a clean state, you can remove the data folder. For convenience, you can use the *clean* argument to the `bin/karaf` Linux script (`binkaraf.bat` on Windows).  
a. On Linux:

    bin/karaf clean  
    bin/start clean
    

b. On Windows:

    binkaraf.bat clean  
    binstart.bat clean
    

**Customize variables**  
Apache Karaf accepts environment variables:

     * JAVA_MIN_MEM: minimum memory for the JVM (default is 128M).
     * JAVA_MAX_MEM: maximum memory for the JVM (default is 512M).
     * JAVA_PERM_MEM: minimum perm memory for the JVM (default is JVM default value).
     * JAVA_MAX_PERM_MEM: maximum perm memory for the JVM (default is JVM default value).
     * KARAF_HOME: the location of your Apache Karaf installation (default is found depending where you launch the startup script).
     * KARAF_BASE: the location of your Apache Karaf base (default is KARAF_HOME).
     * KARAF_DATA: the location of your Apache Karaf data folder (default is KARAF_BASE/data).
     * KARAF_ETC: the location of your Apache Karaf etc folder (default is KARAF_BASE/etc).
     * KARAF_OPTS: extra arguments passed to the Java command line (default is null).
     * KARAF_DEBUG: if 'true', enable the debug mode (default is null). If debug mode is enabled, Karaf starts a JDWP socket on port 5005. You can plug your IDE to define breakpoints, and run step by step.
    

You can define these environment variables in the `bin/setenv` Linux script (`binsetenv.bat` on Windows). For instance, to set the minimum and maximum memory size for the JVM, you can define the following values: a. On Linux: **Content of bin/setenv**

     export JAVA_MIN_MEM=256M
     export JAVA_MAX_MEM=1024M
    

b. On Windows:** rem Content of binsetenv.bat**

     set JAVA_MIN_MEM=256M
     set JAVA_MAX_MEM=1024M
    

**Connecting**  
Even if you start Apache Karaf without the console (using server or background modes), you can connect to the console. This connection can be local or remote, in which case you can access the Karaf console remotely. To connect to the console, you can use the `bin/client` Linux script (`binclient.bat` on Windows).  
a. On Linux:

     /bin/client -u karaf
    

Logging in as karaf 360 [pool-2-thread-3] WARN org.apache.sshd.client.keyverifier.AcceptAllServerKeyVerifier - Server at /0.0.0.0:8101 presented unverified key:

           _________      .__                  
           __________ __|__| ____ __  ___    
             / | ___  V__  |/      /  /    
            /  |  |   |  |  |   |          
            __| / |___|  |__>___|  /_/__   
               /                 /           
    Frinx version: 1.0.0-Beryllium-SR1.2-frinx frinx-user@root>
    

Hit `[tab]` for a list of available commands

Type`[cmd] --help` for help on a specific command.

Type `system:shutdown` to shutdown Karaf.

Hit `<ctrl-d>` or type `logout` to disconnect the shell from the current session.

`karaf@root()>`

b. On Windows:

     binclient.bat -u karaf`
    

Logging in as karaf 360 [pool-2-thread-3] WARN org.apache.sshd.client.keyverifier.AcceptAllServerKeyVerifier - Server at /0.0.0.0:8101 presented unverified key:

           _________      .__                  
           __________ __|__| ____ __  ___    
             / | ___  V__  |/      /  /    
            /  |  |   |  |  |   |          
            __| / |___|  |__>___|  /_/__   
               /                 /           
    Frinx version: 1.0.0-Beryllium-SR1.2-frinx frinx-user@root>
    

Hit `[tab]` for a list of available commands

Type`[cmd] --help` for help on a specific command.

Type `system:shutdown` to shutdown Karaf.

Hit `<ctrl-d>` or type `logout` to disconnect shell from current session.

    karaf@root()>`
    

By default, client tries to connect on localhost, on port 8101 (the default Apache Karaf SSH port). Client accepts different options to let you connect on a remote Apache Karaf instance. You can use --help to get details about these options.

**Help**  
a. On Linux:

    bin/client --help
    

Apache Karaf client

-a [port] specify the port to connect to -h [host] specify the host to connect to -u [user] specify the user name

*   -help shows this help message -v raise verbosity
*   -r [attempts] retry connection establishment (up to attempts times) -d [delay] intra-retry delay (defaults to 2 seconds) -b batch mode, specify multiple commands via standard input -f [file] read commands from the specified file [commands] commands to run

*If no commands are specified, the client will be put into an interactive mode*

b. On Windows:

    binclient.bat --help
    

**Apache Karaf client**  
-a [port] specify the port to connect to -h [host] specify the host to connect to -u [user] specify the user name --help shows this help message -v raise verbosity -r [attempts] retry connection establishment (up to attempts times) -d [delay] intra-retry delay (defaults to 2 seconds) -b batch mode, specify multiple commands via standard input -f [file] read commands from the specified file [commands] commands to run *If no commands are specified, the client will be put in an interactive mode* [/wpmem_form]

 [1]: https://karaf.apache.org/manual/latest/#_integration_in_the_operating_system_the_service_wrapper