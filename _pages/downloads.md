---
ID: 1353
post_title: Downloads
author: frinxeditor
post_excerpt: ""
layout: page
permalink: https://frinx.io/downloads
published: true
post_date: 2016-06-06 15:49:41
---
[av_one_fifth first min_height='' vertical_alignment='' space='' custom_margin='' margin='0px' padding='0px' border='' border_color='' radius='0px' background_color='' src='' background_position='top left' background_repeat='no-repeat' animation=''][/av_one_fifth]

[av_three_fifth min_height='' vertical_alignment='' space='' custom_margin='' margin='0px' padding='0px' border='' border_color='' radius='0px' background_color='' src='' background_position='top left' background_repeat='no-repeat' animation='']

[av_textblock size='' font_color='' color='' custom_class=''] [wpmem_form login]

USER: **[wpmem_field field=user_login]** Please choose from one of the following options to download and run your FRINX OpenDaylight Distribution. The FRINX ODL Distribution is free to use for 30 days. Please contact us at <info@frinx.io> if you want to purchase a commercial license during or after the trial period.

**Download zip file **Please click on the following link to download a zip archive of the FRINX ODL Distribution. By downloading the file you accept the FRINX software [EULA][1]

Boron [distribution-karaf-2.3.0.frinx.zip][2] Beryllium [distribution-karaf-1.4.6.frinx.zip][3]

Last release notes for boron [ Release notes boron][4] Last release notes for beryllium [ Release notes beryllium][5] Download release from archive [Archive][6]

## 

**Start your FRINX ODL Distribution for the first time **Go to the directory where you have unpacked the zip file and enter the following commands on the CLI to activate your installation. *The token below is unique to your user account on frinx.io and can not be shared with other users.*

<pre>bin/karaf frinx.createtoken [frinx-license_secret-token]
</pre>

**Every user on frinx.io has their own token generated for them.** Based on this unique token and basic information about your installation environment, we will authorize your installation of the Frinx ODL distribution and create a local license file on your installation. From then on you will not need to provide the token when starting FRINX.

If you do not have Internet connectivity on the machine that you want to install the FRINX ODL distribution on, please contact us at <support@frinx.io> and we can help you get up and running in no time. Running as a Docker container By downloading the docker image you accept the FRINX software [EULA][1] Starting a new container and activating the license Enter the following commands to start your docker container and activate your installation: for Beryllium

<pre>docker pull frinx/frinx_odl:1.4.6.frinx
TOKEN=[frinx-license_secret-token]
docker run -it --hostname some-hostname --name some-frinx -p 8181:8181 frinx/frinx_odl frinx.createtoken.force $TOKEN
</pre>

for Boron

<pre>docker pull frinx/frinx_odl:2.3.0.frinx
TOKEN=[frinx-license_secret-token]
docker run -it --hostname some-hostname --name some-frinx -p 8181:8181 frinx/frinx_odl frinx.createtoken.force $TOKEN
</pre>

Open the next link in your browser: <http://localhost:8181/index.html> , login with username admin, password admin.

**Note about networking **In the previous example only port 8181 was mapped to the docker host. To access all other ports there are more options, most notably

Use docker0 ethernet bridge By default docker runs with an isolated network interface. From the docker host type:

<pre>docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' some-frinx
</pre>

to get the IP of the running container. You can then access all ports including the web server (8181) using that IP. The IP is accessible only from the docker host, unless routing is set up. Use host networking If you want to map all ports exposed by the image, you can use host networking:

<pre>docker run --net=host ...
</pre>

To the outside world this would be the same as running karaf directly on the host. Advanced networking For these options please refer to the official [Docker networking documentation][7]. Stopping the container As the container was given the name some-frinx, type:

<pre>docker stop some-frinx</pre>

**Committing the container to local images **The previous docker run command created a license file inside the some-frinx container. We recommend creating a docker image by typing:

<pre>docker commit some-frinx frinx/frinx_odl:licensed</pre>

This command will create a new tag - licensed. This image has the frinx license file.

**Starting a stopped container **To start a stopped container, run:

<pre>docker start some-frinx</pre>

**Starting from clean state **After installing some features it might be useful to come back to a clean karaf. If you created the licensed tag, you can simply run:

<pre>docker rm some-frinx
docker run -it --hostname some-hostname --name some-frinx -p 8181:8181 frinx/frinx_odl:licensed
</pre>

**Connecting to the karaf console of a running container **docker exec -it some-frinx bin/client -u karaf

**Troubleshooting and advanced topics:** ** Activating the FRINX ODL Distribution behind a proxy **Please set up java system properties as described here: <https://docs.oracle.com/javase/6/docs/technotes/guides/net/proxies.html>

This means running karaf with something like this:

JAVA_OPTS="-Dhttp.proxyHost=10.0.0.100 -Dhttp.proxyPort=8800" bin/karaf frinx.createtoken ...

**Activating the FRINX ODL Distribution on a server without Internet access **These are the steps required to generate the license on a system without internet access:

Let's call the connected computer ONLINE and the one where you want to run karaf OFFLINE.

<pre>OFFLINE# TOKEN="insert your token here"
OFFLINE# KARAF_HOME="insert path to karaf"
OFFLINE# echo "token=$TOKEN" > $KARAF_HOME/etc/frinx.license.cfg
</pre>

Generate fingerprint json to a local file:

<pre>OFFLINE# $KARAF_HOME/bin/karaf frinx.fingerprint > fingerprint.txt
</pre>

Now, copy fingerprint.txt to the ONLINE machine:

<pre>ONLINE# curl https://license.frinx.io/api/v1/obtain-license -d "@fingerprint.txt"  -H 'Content-Type: application/json' -X PUT > frinx.license.cfg
</pre>

Copy frinx.license.cfg back to the OFFLINE machine, replacing the file in karaf's etc folder.

You will now be able to start karaf normally:

<pre>OFFLINE# $KARAF_HOME/bin/karaf
</pre>

**Anyconnect VPN issue **If karaf fails with the following exceptions, please try stopping anyconnect. For more information see <https://ask.opendaylight.org/question/942/running-karaf/>

      Frinx License warning: Frinx distribution is only supported on Linux
    >
    >         _________      .__
    >         \________\__ __|__| ____ __  ___
    >           / | ___\  V__\  |/    \  \/  /
    >          /  | \ |   |  |  |   |  \    \\
    >          \__| / |___|  |__>___|  /_/\__\\
    >             \/                 \/
    >
    > Frinx version: 1.2.5.frinx
    > frinx-user@root>
    > frinx-user@root>Exception in thread "JMX Connector Thread [service:jmx:rmi://0.0.0.0:44444/jndi/rmi://0.0.0.0:1099/karaf-root]" java.lang.RuntimeException: Could not start JMX connector server
    >        at org.apache.karaf.management.ConnectorServerFactory$1.run(ConnectorServerFactory.java:258)
    > Caused by: java.io.IOException: Cannot bind to URL [rmi://0.0.0.0:1099/karaf-root]: javax.naming.ServiceUnavailableException [Root exception is java.rmi.ConnectException: Connection refused to host: 0.0.0.0; nested exception is:
    >        java.net.ConnectException: Operation timed out]
    >        at javax.management.remote.rmi.RMIConnectorServer.newIOException(RMIConnectorServer.java:827)
    >        at javax.management.remote.rmi.RMIConnectorServer.start(RMIConnectorServer.java:432)
    >        at org.apache.karaf.management.ConnectorServerFactory$1.run(ConnectorServerFactory.java:245)
    > Caused by: javax.naming.ServiceUnavailableException [Root exception is java.rmi.ConnectException: Connection refused to host: 0.0.0.0; nested exception is:
    >        java.net.ConnectException: Operation timed out]
    >        at com.sun.jndi.rmi.registry.RegistryContext.bind(RegistryContext.java:147)
    >        at com.sun.jndi.toolkit.url.GenericURLContext.bind(GenericURLContext.java:228)
    >        at javax.naming.InitialContext.bind(InitialContext.java:425)
    >        at javax.management.remote.rmi.RMIConnectorServer.bind(RMIConnectorServer.java:644)
    >        at javax.management.remote.rmi.RMIConnectorServer.start(RMIConnectorServer.java:427)
    >        ... 1 more
    > Caused by: java.rmi.ConnectException: Connection refused to host: 0.0.0.0; nested exception is:
    >        java.net.ConnectException: Operation timed out
    >        at sun.rmi.transport.tcp.TCPEndpoint.newSocket(TCPEndpoint.java:619)
    >        at sun.rmi.transport.tcp.TCPChannel.createConnection(TCPChannel.java:216)
    >        at sun.rmi.transport.tcp.TCPChannel.newConnection(TCPChannel.java:202)
    >        at sun.rmi.server.UnicastRef.newCall(UnicastRef.java:342)
    >        at sun.rmi.registry.RegistryImpl_Stub.bind(Unknown Source)
    >        at com.sun.jndi.rmi.registry.RegistryContext.bind(RegistryContext.java:141)
    >        ... 5 more
    > Caused by: java.net.ConnectException: Operation timed out
    >        at java.net.PlainSocketImpl.socketConnect(Native Method)
    >        at java.net.AbstractPlainSocketImpl.doConnect(AbstractPlainSocketImpl.java:350)
    >        at java.net.AbstractPlainSocketImpl.connectToAddress(AbstractPlainSocketImpl.java:204)
    >        at java.net.AbstractPlainSocketImpl.connect(AbstractPlainSocketImpl.java:188)
    >        at java.net.SocksSocketImpl.connect(SocksSocketImpl.java:392)
    >        at java.net.Socket.connect(Socket.java:589)
    >        at java.net.Socket.connect(Socket.java:538)
    >        at java.net.Socket.(Socket.java:434)
    >        at java.net.Socket.(Socket.java:211)
    >        at sun.rmi.transport.proxy.RMIDirectSocketFactory.createSocket(RMIDirectSocketFactory.java:40)
    >        at sun.rmi.transport.proxy.RMIMasterSocketFactory.createSocket(RMIMasterSocketFactory.java:148)
    >        at sun.rmi.transport.tcp.TCPEndpoint.newSocket(TCPEndpoint.java:613)
    >        ... 10 more  

[/wpmem_form]

[/av_textblock]

[/av_three_fifth][av_one_fifth min_height='' vertical_alignment='' space='' custom_margin='' margin='0px' padding='0px' border='' border_color='' radius='0px' background_color='' src='' background_position='top left' background_repeat='no-repeat' animation=''][/av_one_fifth]

 [1]: https://frinx.io/wp-content/uploads/2017/01/EULA_ODL_20170104_v102.pdf
 [2]: https://license.frinx.io/download/distribution-karaf-2.3.0.frinx.zip
 [3]: https://license.frinx.io/download/distribution-karaf-1.4.6.frinx.zip
 [4]: https://frinx.io/frinx-documents/frinx-odl-distribution-2.3.0.html
 [5]: https://frinx.io/frinx-documents/frinx-odl-distribution-1.4.6.html
 [6]: https://frinx.io/archive
 [7]: https://docs.docker.com/engine/userguide/networking/dockernetworks/