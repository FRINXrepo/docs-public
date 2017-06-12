---
ID: 2685
post_title: 'Operations &#038; Maintenance'
author: ngray@frinx.io
post_date: 2016-11-16 12:48:02
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/sbe-operations-maintenance.html
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

*   Container maintenance
*   Build scripts description
*   Building project

## 1\. Container maintenance

**Scripts to start and stop containers**

| Command                            | Description                                                                 |
| ---------------------------------- | --------------------------------------------------------------------------- |
| ./sbe ls                           | Show running components                                                     |
| ./sbe start [component]            | Start suite or specified component                                          |
| ./sbe stop [component]             | Stop suite or specified component                                           |
| ./sbe restart [component]          | Restart suite or specified component                                        |
| ./sbe network-create               | Create network                                                              |
| ./sbe network-remove               | Remove network                                                              |
| ./sbe volumes-create [volume-name] | Create volumes or specified volume                                          |
| ./sbe volumes-remove [volume-name] | Remove volumes or specified volume                                          |
| ./sbe proxy-start                  | Start reverse proxy server                                                  |
| ./sbe proxy-stop                   | Stop reverse proxy server                                                   |
| ./sbe proxy-restart                | Restart reverse proxy server                                                |
| ./sbe pull-images [image-name]     | Pull specified component image or all images                                |
| ./sbe instance-update              | Update instance configuration if configuration or project yaml was modified |

**Other commands**

| Command                               | Description                                    |
| ------------------------------------- | ---------------------------------------------- |
| ./sbe run ldap-import [ldif filename] | Tool for importing LDIF file into LDAP service |

**To stop and remove the various containers use**

    ./sbe stop <container-name>
    

**Clean volumes**

*WARNING: The following commands will result in data loss. They are NOT for normal operation and should only be run by an administrator for the purposes of system maintenance.*

    ./sbe volumes-remove [<volume-name>]  
    

## 2\. Build commands description

**Build scripts description**

| Command                  | Description                                  |
| ------------------------ | -------------------------------------------- |
| ./sbe run project-import | Import custom Git repository into SBE Gerrit |
| ./sbe run project-build  | Create jenkins job for build                 |
| ./sbe run project-run    | Run jenkins job remotely                     |

## 3\. Building projects

Import the example project into Gerrit

First import the example project from the public or private repository into Gerrit. Before you continue, set the following variables:

    export PROJECT_NAME="hello-world-samples"
    export PROJECT_UPSTREAM_URL="https://github.com/frinxio/hello-world-samples.git"
    

Add sources from remote Git into Gerrit:

     ./sbe run project-import $PROJECT_NAME $PROJECT_UPSTREAM_URL
    

**Before you run the following command to run and build a Jenkins job, see [here][1] for information on how to define a project.**

Create a Jenkins job to build and run the Jenkins job:

    ./sbe run project-build $PROJECT_NAME <jenkins-username> <jenkins-username-password>
    

## 4\. Cloning individual repositories

The sbe repository is cloned as part of the standard installation procedure. However it is also possible to clone the individual components of the SBE listed in the following table:

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

To clone one of the above repositories, replace xxx with the repository name in the following command:

    git clone https://[customername]@gerrit.frinx.io/xxx
    

When prompted for a password enter the [customerpassword] provided by FRINX.

[/wpmem_form]

 [1]: https://frinx.io/frinx-documents/sbe-project-definition.html