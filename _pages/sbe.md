---
ID: 4170
post_title: FRINX Smart Build Engine
author: frinxadmin
post_excerpt: ""
layout: page
permalink: https://frinx.io/sbe
published: true
post_date: 2017-03-27 11:00:51
---
### FRINX Smart Build Engine (SBE)

***Ready-to-run package for the entire software development process***. A continuous integration and continuous deployment system based on Docker containers, it leverages well-known open source projects and comes pre-integrated to get you up and running quicker. The system can run on one or multiple host VMs.

*Full integration between several well-established open-source solutions for source code management and code review, continuous integration, code quality assessment, project management and repository management.*

***Preconfigured and linked tools mean software teams can embark immediately on the development process***

***Scalable to very large projects and hence suitable for developing forked versions of existing projects.***

*All SBE tools accessible via a single jump-off page.*

For questions and orders please contact our team at <a href="mailto:info@frinx.io" target="_blank">info@frinx.io</a>.

Please see our introductory video [here][1] For full instructions on using the SBE see our [guide][2]

**The SBE Includes:**  
- Docker containers with open source CI/CD components  
- Scripts to configure, deploy and manage containers and applications  
- Scripts for building the FRINX ODL distribution and sample applications  
- Documentation

**Figure 1: SBE components**

![Figure 1: Layers][3]

**Software Build** Building software is an end-to-end process that involves many distinct functions.

**Version Control** The version control function carries out activities such as workspace creation and updating, baselining and reporting. It creates an environment for the build process to run in and captures metadata about the inputs and outputs of the build process to ensure repeatability and reliability. Tools such as Git help with these tasks, for example by providing a means to tag specific points in history as being important.

**Code Quality** This function is responsible for checking that developers have adhered to the seven axes of code quality: comments, unit tests, duplication, complexity, coding rules, potential bugs and architecture & design.

**Compilation** The compilation function turns source files into directly executable or intermediate objects.

**Continuous Integration** Continuous Integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early on. The automated build merges all developer working copies to a shared mainline several times a day.

**Figure 2: Continuous Integration** ![Figure 3: Continuous Integration][4]

### Components Description

**Apache Directory Server** ApacheDS is an extensible and embeddable directory server entirely written in Java, which has been certified LDAPv3 compatible by the Open Group. Besides LDAP it supports Kerberos 5 and the Change Password Protocol. It has been designed to introduce triggers, stored procedures, queues and views to the world of LDAP which has lacked these rich constructs.

**Gerrit Code Review System** Gerrit is a Web-based code review tool built on top of the Git version control system. It is intended to provide a lightweight framework for reviewing every commit before it is accepted into the code base. Changes are uploaded to Gerrit but don’t actually become a part of the project until they’ve been reviewed and accepted. Gerrit supports the standard open source process of submitting patches which are then reviewed by project members before being applied to the code base. However Gerrit also makes it simple for all committers on a project to ensure that changes are checked over before they are applied. Gerrit captures notes and comments about code changes to enable discussion of the change.

Gerrit is a free, Web-based team code collaboration tool. Software developers in a team can review each other's modifications on their source code using a Web browser and approve or reject those changes. It integrates closely with Git, a distributed version control system. The Gerrit code review system with PostgreSQL and OpenLDAP integration are supported.

**Jenkins CI** Jenkins is an open source continuous integration tool written in Java. Jenkins provides continuous integration services for software development. It is a server-based system running in a servlet container such as Apache Tomcat. The official Jenkins Docker is used in conjunction with additional plugins and scripts in order to integrate with Gerrit. Additional components include:

**Sonatype Nexus** Nexus is a repository manager. It allows you to proxy, collect, and manage your dependencies so that you are not constantly juggling a collection of JARs. It makes it easy to distribute your software. Internally, you configure your build to publish artifacts to Nexus and they then become available to other developers.

**PostgreSQL** PostgreSQL is a powerful, open source object-relational database system. It has more than 15 years of active development and a proven architecture that has earned it a strong reputation for reliability, data integrity, and correctness. It runs on all major operating systems.

**Redmine** is a free and open source, Web-based project management and issue tracking tool. It allows users to manage multiple projects and associated subprojects. It features per project wikis and forums, time tracking, and flexible, role-based access control.

**NGINX** NGINX is a free, open-source, high-performance HTTP server and reverse proxy, as well as an IMAP/POP3 proxy server. NGINX is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption.

**SBE** A useful container which includes all tools and utilities for working with SBE.

**SonarQube** Provides an overview of the overall health of your source code and even more importantly, it highlights issues found with new code. With a Quality Gate set on your project, you can simply fix the Leak and start mechanically improving.

 [1]: https://www.useloom.com/share/f4ce6cc0e96011e69309454fac1abeab
 [2]: https://frinx.io/frinx-documents/sbe-intro.html
 [3]: https://frinx.io/wp-content/uploads/2016/10/layers.png "Figure 1: Layers"
 [4]: https://frinx.io/wp-content/uploads/2016/10/ci_flow.png "Figure 2: Continuous Integration"