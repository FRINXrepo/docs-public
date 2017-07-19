---
ID: 5147
post_title: L3VPN user guide postman collection.json
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-documents/l3vpn-user-guide-postman-collection-json.html
published: true
post_date: 2017-07-19 11:01:33
---
    {
       "variables": [],
       "info": {
           "name": "ODL_CLI copy",
           "_postman_id": "b78d0b28-cc71-06d6-bb63-fa81622413eb",
           "description": "",
           "schema": "https://schema.getpostman.com/json/collection/v2.0.0/collection.json"
       },
       "item": [
           {
               "name": "CLI registry",
               "description": "",
               "item": [
                   {
                       "name": "TRANSLATE REGISTRY",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/cli-translate-registry:available-cli-device-translations",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": ""
                           },
                           "description": ""
                       },
                       "response": []
                   }
               ]
           },
           {
               "name": "Cli topology",
               "description": "",
               "item": [
                   {
                       "name": "List CLI topology OPER",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n  \"input\" :\n  {\n     \"ios-cli:command\" : \"ls ~\"\n  }\n}"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "List CLI topology CFG",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n  \"input\" :\n  {\n     \"ios-cli:command\" : \"ls ~\"\n  }\n}"
                           },
                           "description": ""
                       },
                       "response": []
                   }
               ]
           },
           {
               "name": "Ios mount",
               "description": "",
               "item": [
                   {
                       "name": "Mount SSH",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/IOS1",
                           "method": "PUT",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n    \"network-topology:node\" :\n    {\n      \"network-topology:node-id\" : \"IOS1\",\n      \n      \"cli-topology:host\" : \"172.16.11.112\",\n      \"cli-topology:port\" : \"22\",\n      \"cli-topology:transport-type\" : \"ssh\",\n      \n      \"cli-topology:device-type\" : \"ios\",\n      \"cli-topology:device-version\" : \"*\",\n      \n      \"cli-topology:username\" : \"cisco\",\n      \"cli-topology:password\" : \"cisco\"\n      \n    }\n  }"
                           },
                           "description": "To enable SSH on IOS use:\n\nhttps://networklessons.com/cisco/ccna-routing-switching-icnd1-100-105/configure-ssh-cisco-ios/\n\n\ntelnet <IP>\n enable\n configure terminal\n hostname R1\n ip domain-name NETWORKLESSONS.LOCAL\n crypto key generate rsa\n  1024\n ip ssh version 2\n line vty 0 4\n  transport input ssh\n  login local\n  exit\n username cisco password cisco\n exit"
                       },
                       "response": []
                   },
                   {
                       "name": "Mount TELNET",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/IOS1",
                           "method": "PUT",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n    \"network-topology:node\" :\n    {\n      \"network-topology:node-id\" : \"IOS1\",\n      \n      \"cli-topology:host\" : \"172.16.11.112\",\n      \"cli-topology:port\" : \"22\",\n      \"cli-topology:transport-type\" : \"ssh\",\n      \n      \"cli-topology:device-type\" : \"ios\",\n      \"cli-topology:device-version\" : \"*\",\n      \n      \"cli-topology:username\" : \"cisco\",\n      \"cli-topology:password\" : \"cisco\"\n      \n    }\n  }"
                           },
                           "description": "To enable Telnet on IOS use:\n\nhttp://www.technig.com/enable-telnet-and-ssh-on-cisco-router/"
                       },
                       "response": []
                   },
                   {
                       "name": "Check status",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n    \"network-topology:node\" :\n    {\n      \"network-topology:node-id\" : \"Linux1\",\n      \n      \"cli-topology:host\" : \"10.10.199.226\",\n      \"cli-topology:port\" : \"22\",\n      \"cli-topology:transport-type\" : \"ssh\",\n      \n      \"cli-topology:device-type\" : \"*\",\n      \"cli-topology:device-version\" : \"*\",\n      \n      \"cli-topology:username\" : \"root\",\n\t  \"cli-topology:password\" : \"frinx2017\"\n      \n    }\n  }"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Get Version OPER",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/ios-essential:version",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": ""
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Get Interfaces OPER",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/ios-essential:interfaces",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": ""
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Get Vrfs OPER",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/ios-essential:vrfs",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": ""
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Get all OPER",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": ""
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Get all CONFIG",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "    <vrf xmlns=\"urn:opendaylight:params:xml:ns:yang:ios-cli\">\n        <id>2</id>\n        <address-type>random</address-type>\n        <unicast>no</unicast>\n    </vrf>"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Add new Vrf",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/ios-essential:vrfs",
                           "method": "POST",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/xml",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/xml",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "<vrf xmlns=\"urn:opendaylight:params:xml:ns:yang:ios:essential\">\n    <id>VRFfromPOSTMAN</id>\n    <description>Description</description>\n</vrf>"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Delete Vrf",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/ios-essential:vrfs/vrf/VRFfromPOSTMAN",
                           "method": "DELETE",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/xml",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/xml",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": ""
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Get Vrfs using generic RPC",
                       "request": {
                           "url": "http://localhost:8181/restconf/operations/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/cli-unit-generic:execute-and-read",
                           "method": "POST",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n  \"input\" :\n  {\n     \"ios-cli:command\" : \"sh ip vrf\"\n  }\n}"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "RECONCILE",
                       "request": {
                           "url": "http://localhost:8181/restconf/operations/network-topology:network-topology/topology/cli/node/IOS1/yang-ext:mount/reconcile:reconcile",
                           "method": "POST",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n  \"input\" : {\n  \t\"strategy\": \"merge-from-device\"\n  }\n}"
                           },
                           "description": ""
                       },
                       "response": []
                   }
               ]
           },
           {
               "name": "Ios mount GENERIC",
               "description": "",
               "item": [
                   {
                       "name": "Mount",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/IOS2",
                           "method": "PUT",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n    \"network-topology:node\" :\n    {\n      \"network-topology:node-id\" : \"IOS2\",\n      \n      \"cli-topology:host\" : \"172.16.11.112\",\n      \"cli-topology:port\" : \"22\",\n      \"cli-topology:transport-type\" : \"ssh\",\n      \n      \"cli-topology:device-type\" : \"*\",\n      \"cli-topology:device-version\" : \"*\",\n      \n      \"cli-topology:username\" : \"cisco\",\n\t  \"cli-topology:password\" : \"cisco\"\n      \n    }\n  }"
                           },
                           "description": "To enable SSH on IOS use:\n\nhttps://networklessons.com/cisco/ccna-routing-switching-icnd1-100-105/configure-ssh-cisco-ios/\n\n\ntelnet <IP>\n enable\n configure terminal\n hostname R1\n ip domain-name NETWORKLESSONS.LOCAL\n crypto key generate rsa\n  1024\n ip ssh version 2\n line vty 0 4\n  transport input ssh\n  login local\n  exit\n username cisco password cisco\n exit"
                       },
                       "response": []
                   },
                   {
                       "name": "Check status",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/IOS2",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n    \"network-topology:node\" :\n    {\n      \"network-topology:node-id\" : \"Linux1\",\n      \n      \"cli-topology:host\" : \"10.10.199.226\",\n      \"cli-topology:port\" : \"22\",\n      \"cli-topology:transport-type\" : \"ssh\",\n      \n      \"cli-topology:device-type\" : \"*\",\n      \"cli-topology:device-version\" : \"*\",\n      \n      \"cli-topology:username\" : \"root\",\n\t  \"cli-topology:password\" : \"frinx2017\"\n      \n    }\n  }"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Show interfaces",
                       "request": {
                           "url": "http://localhost:8181/restconf/operations/network-topology:network-topology/topology/cli/node/IOS2/yang-ext:mount/cli-unit-generic:execute-and-read",
                           "method": "POST",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n  \"input\" :\n  {\n     \"ios-cli:command\" : \"sh ip inter brie\"\n  }\n}"
                           },
                           "description": ""
                       },
                       "response": []
                   }
               ]
           },
           {
               "name": "Linux mount",
               "description": "",
               "item": [
                   {
                       "name": "Mount SSH",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/Linux1",
                           "method": "PUT",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n    \"network-topology:node\" :\n    {\n      \"network-topology:node-id\" : \"Linux1\",\n      \n      \"cli-topology:host\" : \"10.10.199.226\",\n      \"cli-topology:port\" : \"22\",\n      \"cli-topology:transport-type\" : \"ssh\",\n      \n      \"cli-topology:device-type\" : \"*\",\n      \"cli-topology:device-version\" : \"*\",\n      \n      \"cli-topology:username\" : \"root\",\n\t  \"cli-topology:password\" : \"frinx2017\"\n      \n    }\n  }"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Mount TELNET",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/Linux1",
                           "method": "PUT",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n    \"network-topology:node\" :\n    {\n      \"network-topology:node-id\" : \"Linux1\",\n      \n      \"cli-topology:host\" : \"192.168.1.151\",\n      \"cli-topology:port\" : \"23\",\n      \"cli-topology:transport-type\" : \"telnet\",\n      \n      \"cli-topology:device-type\" : \"*\",\n      \"cli-topology:device-version\" : \"*\",\n      \n      \"cli-topology:username\" : \"mmarsalek\",\n\t  \"cli-topology:password\" : \"frinx2017\"\n      \n    }\n  }"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Check status",
                       "request": {
                           "url": "http://localhost:8181/restconf/operational/network-topology:network-topology/topology/cli/node/Linux1",
                           "method": "GET",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n    \"network-topology:node\" :\n    {\n      \"network-topology:node-id\" : \"Linux1\",\n      \n      \"cli-topology:host\" : \"10.10.199.226\",\n      \"cli-topology:port\" : \"22\",\n      \"cli-topology:transport-type\" : \"ssh\",\n      \n      \"cli-topology:device-type\" : \"*\",\n      \"cli-topology:device-version\" : \"*\",\n      \n      \"cli-topology:username\" : \"root\",\n\t  \"cli-topology:password\" : \"frinx2017\"\n      \n    }\n  }"
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "Unmount",
                       "request": {
                           "url": "http://localhost:8181/restconf/config/network-topology:network-topology/topology/cli/node/Linux1",
                           "method": "DELETE",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": ""
                           },
                           "description": ""
                       },
                       "response": []
                   },
                   {
                       "name": "List home directory",
                       "request": {
                           "url": "http://localhost:8181/restconf/operations/network-topology:network-topology/topology/cli/node/Linux1/yang-ext:mount/cli-unit-generic:execute-and-read",
                           "method": "POST",
                           "header": [
                               {
                                   "key": "Authorization",
                                   "value": "Basic YWRtaW46YWRtaW4=",
                                   "description": ""
                               },
                               {
                                   "key": "Accept",
                                   "value": "application/json",
                                   "description": ""
                               },
                               {
                                   "key": "Content-Type",
                                   "value": "application/json",
                                   "description": ""
                               }
                           ],
                           "body": {
                               "mode": "raw",
                               "raw": "{\n  \"input\" :\n  {\n     \"ios-cli:command\" : \"ls ~\"\n  }\n}"
                           },
                           "description": ""
                       },
                       "response": []
                   }
               ]
           }
       ]
    }