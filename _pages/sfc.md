---
ID: 3266
post_title: >
  Pluggable Service Function Chaining
  Solution
author: ngray@frinx.io
post_date: 2016-12-06 11:11:38
post_excerpt: ""
layout: page
permalink: https://frinx.io/sfc
published: true
sidebar:
  - 'a:1:{i:0;s:0:"";}'
footer:
  - 'a:1:{i:0;s:0:"";}'
header_title_bar:
  - 'a:1:{i:0;s:0:"";}'
header_transparency:
  - 'a:1:{i:0;s:0:"";}'
---
### Problem Definition:

Provide a common modular architecture for service chaining across OpenStack and Kubernetes

### Solution Summary:

Leverage Service Function Chaining and Group Based Policy code in ODL and provide plugins in OpenStack and Kubernetes. Make SFC service catalogue in ODL accessible by Cloudify.

### How is this different than xyz?

Entirely based on open source components no dependency on vendor roadmaps and goals. Provides pluggable architecture to create container and VM based service chains with popular cloud orchestration platforms. Provides integration with Cloudify.

![1]

[1]: https://github.com/ndgray/Images/blob/master/cdn.png" Figure 1: CDN"