---
ID: 3704
post_title: Updating SBE components
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/component-guide.html
published: true
post_date: 2017-01-23 13:59:36
---
This guide explains how to update the SBE - both in its entirety and on a component-by-component basis.

### Updating SBE core

Move to the SBE main project directory

    cd sbe
    

Check the release and current version of SBE sources

    cat sbe.release
    

Alternatively, you can use the following command, which also lists the Docker version

    ./sbe -v
    

Use this command to pull new changes from the SBE remote (FrinxIO) repository

    git pull
    

**You will be prompted for a password - please use the password issued by FRINX. If you do not have a password please contact info@frinx.io**

Please read the **ChangeLog.txt** text file (within your sbe directory). It provides details of SBE news and changes/fixes.

Next, back up your data for each of the SBE components.

If you would like to download new images for all of the SBE components, go to your ~/sbe directory and enter the following command in a terminal

**Warning: Before you update the SBE or one of its components, ensure nobody is currently using any of the SBE components to be updated**

    ./sbe pull-images   
    

If there have been any changes to the image, Docker will update your local image(s).

### Updating individual SBE components

If you only wish to update the image for one particular component, do the following:

Stop the component container which you wish to update - use the following command

    ./sbe stop COMPONENT-NAME
    

e.g.:

    ./sbe stop jenkins    
    

To ensure the container was stopped, use the command

    ./sbe ls  
    

or

    docker ps
    

**Warning: Before you update the SBE or one of its components, ensure nobody is currently using any of the SBE components to be updated**

To update the component

    ./sbe pull-images COMPONENT-IMAGE-NAME
    

Where COMPONENT-IMAGE-NAME takes the following format:

sbe-[component]-version

e.g.

    ./sbe pull-images sbe-jenkins-x3
    

Now start the component container using the command:

    ./sbe start COMPONENT-NAME
    

e.g.:

    ./sbe start jenkins
    

Test the SBE funcionality (create, import, build project, test for each component) using the command

    ./test-hello-world-samples
    

This is a test script which checks all SBE functionality.

### Customizing the SBE component Docker image (And updating it from a self-owned Docker Repository)

Stop the component container using the command

    ./sbe stop COMPONENT-NAME  
    

e.g.:

    ./sbe stop jenkins
    

First clone the Docker image for the repository:

Move to your root sbe directory. To clone one of the repositories listed below, replace xxx with the repository name in the following command:

    git clone https://[customername]@gerrit.frinx.io/xxx
    

When prompted for a password enter the [customerpassword] provided by FRINX.

| COMPONENT   | REPOSITORY NAME        |
| ----------- | ---------------------- |
| apacheds    | sbe-docker-apacheds    |
| base        | sbe-docker-base        |
| gerrit      | sbe-docker-gerrit      |
| jenkins     | sbe-docker-jenkins     |
| nexus       | sbe-docker-nexus       |
| nginx       | sbe-docker-nginx       |
| postgresql  | sbe-docker-postgresql  |
| redmine     | sbe-docker-redmine     |
| sbe         | sbe-docker-sbe         |
| nginx-proxy | sbe-docker-nginx-proxy |
| sonarqube   | sbe-docker-sonarqube   |

This will create a directory in your root sbe directory.

Move into the component project repository directory (all Docker component projects have the prefix: sbe-docker-*)

For example

    cd sbe-docker-jenkins
    

Create your custom change/changes to the image.

**Edit the file name "VERSION" (located in the component project directory): replace the version tag with one of your choosing.**

**Edit the file named "IMAGE" (located in the component project directory): replace the Docker Repository name and/or image name with ones of your choosing.**

Still within the component project repository directory, create/build the Docker image using the command:

    make
    

Wait for a successful build...

Next you must log in to Docker using your Docker credentials

    docker login  
    

If the build was a success then you can now push the created Docker image into Your Docker Repository using the command:

    make push
    

**Now change the image version and/or image name in the "sbe.images" configuration file (located in the root sbe core directory)**

Now we can try starting the component using the new image. First create the network

    ./sbe network-create
    

How start the component container using the command

    ./sbe start COMPONENT-NAME
    

e.g.:

    ./sbe start jenkins    
    

Make sure your new version of the component starts using

    ./sbe ls
    

You should see your new version listed.