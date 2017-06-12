---
ID: 4536
post_title: FRINX VPP distribution
author: frinxadmin
post_date: 2017-05-29 13:27:33
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-vpp-distribution/frinx-vpp-distribution.html
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
FRINX provides an FD.io distribution.  
FD.io is an opensource project that among other things provides the Vector Packet Processor. More information at [FD.io][1].  
This page contains the details about FRINX fd.io distribution.

# Features

Project imported from open source:

*       VPP 
    *   No changes

Internal projects:

*       VPP-monitoring-agent (magent)

# Operations

## CI/CD

There is a custom CI/CD pipeline for FRINX fd.io distribution. It is based on [<span class="confluence-link">SBE</span> ][2].  
The following diagram shows the relationships between FD.io and FD.FRINX.io:

<img src="https://frinx.io/wp-content/uploads/2017/05/fdio.png" alt="" width="1031" height="991" class="alignleft size-full wp-image-4458" />

## SBE installation

Refer to <ac:link><ri:page ri:space-key="SBE" ri:content-title="SBE FDio" ri:version-at-save="14" /><ac:link-body><span class="confluence-link">SBE for FDio installation</span> </ac:link-body></ac:link> page for install instructions.

## Deployment

The CI/CD lives in a dedicated VM inside Siecit.

The credentials and access is listed at the [<span class="confluence-link">credentials page</span> ][3]

The static IPs can be found at [IP allocation page][4]

## Public access

*   [gerrit.fd.frinx.io][5] 
    *   Not publicly browse-able
*   [jenkins.fd.frinx.io][6] 
    *   Not publicly browse-able
*   [nexus.fd.frinx.io][7] 
    *   Publicly browse-able

<ac:structured-macro ac:name="note" ac:schema-version="1" ac:macro-id="38d9de58-9bf6-4177-b1b1-cdaf679fa776"><ac:rich-text-body>

Admin credentials for the services: **admin** (password: **sbe4fdio,** )

</ac:rich-text-body></ac:structured-macro>

# Installing binary packages

Instructions for consuming publicly available binary packages of FD.FRINX.io distribution

## Centos7

In file:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="d6134dc1-a401-4f8d-a2a2-27a6b996a708"><ac:plain-text-body>/etc/yum.repos.d/frinx-fdio-release.repo</ac:plain-text-body></ac:structured-macro>

Set content:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="337aad8b-dd55-48e1-bba7-70124de0bd70"><ac:plain-text-body>[frinx-fdio-release] name=FRINX fd.io release branch latest merge baseurl=https://<CustomerID>:<CustomerPassword>@nexus.fd.frinx.io/nexus/content/repositories/fd.io.centos7/ enabled=1 gpgcheck=0 sslverify=0</ac:plain-text-body></ac:structured-macro>

<p class="auto-cursor-target">
  <br />
</p>

<ac:structured-macro ac:name="warning" ac:schema-version="1" ac:macro-id="3ea9f650-5095-4365-b52d-8234bf9ecf7e"><ac:rich-text-body>

Make sure to change the CustoemrID and password in the repository settings !!!

</ac:rich-text-body></ac:structured-macro>

And the installation with YUM should be:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="a0e1c792-2661-4a34-8b6e-5e639f5b3266"><ac:plain-text-body>sudo yum install vpp vpp-plugins vpp-monitoring-agent</ac:plain-text-body></ac:structured-macro>

# Jenkins jobs

The following diagrams list the jenkins jobs imported from opensource FD.io (green marks imported):

<img src="https://frinx.io/wp-content/uploads/2017/05/vpp.png" alt="" width="1143" height="461" class="alignleft size-full wp-image-4459" />

How-Tos

## Releasing

The basic setup does not take care of release process. Releases have to be managed manually.

Basically, once we are happy with packages in the stable repository, we need to manually copy the over into a **release** repository.

## FDio sync

There is no automated sync between FDio codebases and FRINX's FDio forks.

In order to perform a sync, use the import_fdio.sh script from ci-management/frinx. It will update all specified projects, all branches.

Then triggering required merge jobs would build and deploy all the packages.

## Adding customer account

Create the account by creating a an ldif file in the sbe container:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="6c68ef30-d794-4267-8001-d0a377edb28b"><ac:plain-text-body>docker exec -it sbe-FDio-sbe vi /data/instances/FDio/ldap/customer.ldif</ac:plain-text-body></ac:structured-macro>

and pasting following content:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="48dc4500-50c2-4215-a1f9-806490eec6ec"><ac:plain-text-body>dn: uid=customer,ou=accounts,dc=example,dc=com objectClass: inetOrgPerson objectClass: organizationalPerson objectClass: person uid: customer cn: Generic Customer displayName: Generic Customer sn: customer givenName: Customer mail: nobody@exists.like.this userpassword: customer</ac:plain-text-body></ac:structured-macro>

<ac:structured-macro ac:name="note" ac:schema-version="1" ac:macro-id="05d4d892-f222-4c47-b04f-8f28ba70dadf"><ac:rich-text-body>

Make sure to update the password

</ac:rich-text-body></ac:structured-macro>

Save the file and invoke following command:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="f150a96a-3471-4ec8-84a0-8ffd3936950b"><ac:plain-text-body>./sbe -i FDio run ldap-import customer.ldif</ac:plain-text-body></ac:structured-macro>

This will create the customer account. Delete the customer.ldif file from container.

### Adding to customers group

Similarly to before, create ldif file:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="3a02fe07-bd50-4ece-b5e9-e8de0cfe6869"><ac:plain-text-body>docker exec -it sbe-FDio-sbe vi /data/instances/FDio/ldap/customerToGroup.ldif</ac:plain-text-body></ac:structured-macro>

and set the content to:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="6106a7c1-22eb-447a-aaa8-5bda3aa5f55e"><ac:plain-text-body>dn: cn=customers,ou=accounts,dc=example,dc=com objectClass: groupOfNames objectClass: top cn: customers member: uid=customer,ou=accounts,dc=example,dc=com</ac:plain-text-body></ac:structured-macro>

and ivoke the update:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="3b143b68-e010-4910-8143-a32207cf941d"><ac:plain-text-body>./sbe -i FDio run ldap-import customerToGroup.ldif</ac:plain-text-body></ac:structured-macro>

In case the group already exists, set the content of customerToGroup to:

<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="88e5e6ba-025b-4571-9379-c4dcba6cd6ae"><ac:plain-text-body>dn: cn=customers,ou=accounts,dc=example,dc=com changetype: Modify add: member member: uid=customer2,ou=accounts,dc=example,dc=com</ac:plain-text-body></ac:structured-macro>

and make sure to **remove switch '-a' from ldap-import script in sbe container**

### Configuring customers group rights

#### Nexus

In nexus open LDAP configuration and set the group mapping to:

<img src="https://frinx.io/wp-content/uploads/2017/05/ldapConfigGroup.png" alt="" width="676" height="236" class="alignleft size-full wp-image-4460" />

Next go to **Roles **configuration and add an external mapping for **LDAP:customers** group and set its privileges to:

*   All Repositories (view)
*   All Repositories (read)
*   UI: Base UI
*   UI: Repository browser
*   UI: Search
*   Nexus YUM reader

and save.

Now its important to **disable Anonymous access** in the Server configuration in order to have customer private nexus repositories.

#### Jenkins

Jenkins default LDAP configuration is ready for the account groups. Enabling read only access to **customers** group can be configured in Global Security Settings under Authorization section:

<img src="https://frinx.io/wp-content/uploads/2017/05/ldapJ.png" alt="" width="1851" height="398" class="alignleft size-full wp-image-4461" />

# Resources [1][1]: http://fd.io

[Diagrams on draw.io][8]

[ci-management fork for FD.FRINX.io][9]

 [1]: http://fd.io
 [2]: https://frinx.io/frinx-documents/sbe-intro.html
 [3]: https://phabricator.frinx.io/w/credentials/
 [4]: https://phabricator.frinx.io/w/siecit_support_documentation/static_ip_allocations/
 [5]: http://gerrit.fd.frinx.io
 [6]: http://jenkins.fd.frinx.io
 [7]: http://nexus.fd.frinx.io
 [8]: https://drive.google.com/file/d/0B0qEUdi_UHSpcUlKSXNrLWJMV1k/view?usp=sharing
 [9]: https://gerrit.frinx.io/#/admin/projects/ci-management