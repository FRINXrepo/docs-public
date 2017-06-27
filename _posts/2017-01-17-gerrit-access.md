---
ID: 3623
post_title: Gerrit Access and Administration
author: frinxadmin
post_date: 2017-01-17 08:22:38
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/gerrit-access.html
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
The FRINX SBE uses Git and Gerrit for code review and version control.

Git is a distributed version control system. Once a user clones a Git repository, he has a fully functioning copy of the source code, with all the branches and tagged releases at his disposal. Git supports ssh and http.

Gerrit is a Web-based code review system which aims to improve code by allowing team members to read and comment on it and review it before it is accepted into the existing code base. Gerrit is a Git server and provides access control for the hosted Git repositories and a Web front-end for doing code review. Gerrit's main feature is the ability to view code versions side-by-side for comparing differences and commenting.

Note that while code review is a core part of Gerrit functionality, it is optional. The typical basic Gerrit workflow Gerrit involves two stages: First, the contributor uploads Changes to Gerrit with Git. Second, peers use the Web browser to make reviews.

The following guide focuses on the administration of Gerrit.

### Creating a new user group in Gerrit

**Creating a new user via the Gerrit user interface**  
To see the existing user groups:  
*Click on* **People**  
*Click on* **List Groups**

To create a new group:  
*Click on* **People**  
*Click on* **Create New Group**. For the purposes of an example we can develop throughout this guide, give the group the name "Committers".

Under **Members** you can enter the first few characters of a user's email address. Gerrit will recognize the user and you can click **add** to add that user to the group.

**Note**:  
1\. The user must have logged in to Gerrit at least once in order that the user appears in the list.  
2\. If the user has logged in but nonetheless does not appear, then it is necessary to import the user into ldap:  
3\. In **~/sbe/instances/default/ldap/** copy base.ldif and save as a new name, keeping the .ldif suffix, for example **new-users.ldif**. In the new file, add entries for the new user(s) you wish to add.

The format should be as follows:

    dn: uid=jbloggs,ou=accounts,dc=example,dc=com  
    objectClass: inetOrgPerson  
    objectClass: organizationalPerson  
    objectClass: person  
    uid: jbloggs  
    cn: Joe Bloggs  
    displayName: Joe Bloggs  
    sn: jbloggs  
    givenName: Joe  
    mail: jbloggs@example-email.com  
    userpassword: passwd
    

More instructions on the format can be found in Step 6 here: <https://frinx.io/frinx-documents/sbe-installation.html>

Then, from within your sbe directory, run:

    ./sbe instance-update 
    ./sbe run ldap-import [filename].ldif  
    

Now create another new group called "Contributors". The purpose of creating two groups is so that we can later assign different access rights to the two groups.

**Creating a new user group via the command line**

Alternatively, you can create new groups and add existing users to them via the command line.

First we need to add an SSH public key to Gerrit:

1.  On the right of your Gerrit screen *click on your username and then on* **Settings** 
2.  On the left of the screen, *click on* **SSH Public Keys** 
3.  *Click on the arrow beside* **How to generate an SSH key** and follow the listed steps.
4.  Finally, in a terminal run:
    
    `ssh-add`

To create a new account group called Committers with initial members committer1 and committer2:

    ssh -p 29418 admin@[localhost] gerrit create-group --member committer1 --member committer2 Committers
    

*Replace `[localhost]` with whatever is set as hostname in ~/sbe/instances/default/config*

### Creating a project in Gerrit

**Creating a project via the Gerrit user interface**  
*Click on* **Projects**  
*Click on* **Create New Project**  
Enter a project Name  
Optional: In **Rights Inherit From** choose a project. (see below for more info on access control rights and setting these up)

**Creating a project via the command line**

This can be done as follows:

    ssh -p 29418 admin@[localhost] gerrit create-project example-name
    

*Replace `[localhost]` with whatever is set as hostname in ~/sbe/instances/default/config*

It is also possible to import a project from public git:

    ./sbe run project-import [project name] [URL]
    

Projects added via the command line will be viewable in the Gerrit interface.

### Configuring Gerrit Access Control Lists

Gerrit works on the basis that users who have different roles in a software project (such as developer (committer) or contributor) should have different access rights in Gerrit.

We can dictate which users can push code into a repository and what branches particular users can see. You can also choose which branches are visible to which people. By default, no permissions beyond project ownership are assigned.

In Gerrit, the project owner has permission to edit the access control list and the project settings for a project. Being project owner means being responsible for the administration of a project.

You are able to set up access control according to how you wish your project to operate.

As an example, we can set up access rights for the two Gerrit groups we created as follows:

Users in group **Committers**

-can push commits -can make code-reviews  
-can make merges

Users in group **Contributors**

-can only push commits

**Setting access rights via the Gerrit user interface**

Go to **Projects > List** and *click on your project*  
*Click on* **Access** in the second-row menu near the top of the screen  
*Click on* **Edit**

Here you can configure, add and remove different types of access right for different groups. For example, you can add a group e.g. Committers, and allow *Push*, and allow *Label Code-Review* between -2 and +2. To see what additional permissions you can set, click on *Add Permission* and select for example *Push Merge Commit*.

For any listed permission type you can click on **Add Group**. For example *Push* is already listed. Under Push you can click on **Add Group** and select Contributors.

*Click on* **Save Changes**

Optionally you can provide a commit Message to explain the reasons for changing the access rights.

Access rights are stored in the project’s Git repository in a special branch called refs/meta/config. On this branch there is a project.config file which contains the access rights.

By looking at the history of the project.config file you can see how the access rights were changed and by whom.

**Reviewers**  
Normally it is not necessary to explicitly assign reviewers to every change since the project members either watch the project and get notified by email or regularly check the list of open changes in the Gerrit Web UI. The project members then pick the changes themselves that are interesting to them for review.

If authors of changes want to have a review by a particular person they can request the review by adding this person in the Gerrit Web UI as a reviewer on the change. Gerrit will then notify this person by email about the review request.

### Gerrit terminology

**Change**  
Results in a single commit when merged to the Git repository. Change numbers are unique and never change.

**Score**  
A value in an Approval Category. Indicates if a Change is approved and can be submitted to the Git repository.

**Submit**  
an action that allows Gerrit to merge a Change to the Git repository.

**Abandon**  
Action that archives a Change. An abandoned Change can be restored later.

**Project**  
A Git repository.