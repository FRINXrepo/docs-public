---
ID: 5142
post_title: L3VPN Postman collection JSON
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/uncategorized/l3vpn-postman-collection-json-2.html
published: true
post_date: 2017-07-19 10:27:57
---
test

    {
        "variables": [],
        "info": {
            "name": "L3VPN IOS XRv",
            "_postman_id": "8aff2ee0-8467-4a12-3afe-36b1756d5554",
            "description": "",
            "schema": "https://schema.getpostman.com/json/collection/v2.0.0/collection.json"
        },
        "item": [
            {
                "name": "NETCONF connection",
                "description": "",
                "item": [
                    {
                        "name": "connect pe1",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/pe1",
                            "method": "PUT",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                                "raw": "{\n  \"node\": [\n    {\n      \"node-id\": \"pe1\",\n      \"netconf-node-topology:host\": \"172.16.11.1\",\n      \"netconf-node-topology:port\": 830,\n      \"netconf-node-topology:keepalive-delay\": 0,\n      \"netconf-node-topology:tcp-only\": false,\n      \"netconf-node-topology:username\": \"cisco\",\n      \"netconf-node-topology:password\": \"cisco\"\n    }\n  ]\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "connect pe2",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/pe2",
                            "method": "PUT",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                                "raw": "{\n  \"node\": [\n    {\n      \"node-id\": \"pe2\",\n      \"netconf-node-topology:host\": \"172.16.11.2\",\n      \"netconf-node-topology:port\": 830,\n      \"netconf-node-topology:keepalive-delay\": 0,\n      \"netconf-node-topology:tcp-only\": false,\n      \"netconf-node-topology:username\": \"cisco\",\n      \"netconf-node-topology:password\": \"cisco\"\n    }\n  ]\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "topology-netconf OPER",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/operational/network-topology:network-topology/topology/topology-netconf",
                            "method": "GET",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Accept",
                                    "value": "application/yang.data+json",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{\r\n  \"input\":{\r\n  }\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "topology-netconf CONF",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf",
                            "method": "GET",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Accept",
                                    "value": "application/yang.data+json",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{\r\n  \"input\":{\r\n  }\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "disconnect pe1",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/pe1",
                            "method": "DELETE",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                        "name": "disconnect pe2",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/topology-netconf/node/pe2",
                            "method": "DELETE",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                "name": "ODL",
                "description": "",
                "item": [
                    {
                        "name": "l3vpn-svc",
                        "request": {
                            "auth": {
                                "type": "basic",
                                "basic": {
                                    "username": "admin",
                                    "password": "admin",
                                    "saveHelperData": true,
                                    "showPassword": false
                                }
                            },
                            "url": "http://{{odl_ip}}:8181/restconf/config/ietf-l3vpn-svc:l3vpn-svc",
                            "method": "GET",
                            "header": [
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                },
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{  \r\n  \"l3vpn-svc\":{  \r\n    \"vpn-services\":{  \r\n      \"vpn-service\":[  \r\n        {  \r\n          \"vpn-id\":\"frinxVPN\",\r\n          \"customer-name\":\"frinx\",\r\n          \"vpn-service-topology\":\"any-to-any\",\r\n          \"l3vpn-param:vrf-name\":\"vrf-CE3\",\r\n          \"l3vpn-param:route-distinguisher\":{  \r\n            \"as\":3,\r\n            \"as-index\":3\r\n          },\r\n          \"l3vpn-param:import-route-targets\":{  \r\n            \"route-target\":{  \r\n              \"as\":3,\r\n              \"as-index\":3\r\n            }\r\n          },\r\n          \"l3vpn-param:export-route-targets\":{  \r\n            \"route-target\":{  \r\n              \"as\":3,\r\n              \"as-index\":3\r\n            }\r\n          }\r\n        }\r\n      ]\r\n    },\r\n    \"sites\":{  \r\n      \"site\":[  \r\n        {  \r\n          \"site-id\":\"CE31\",\r\n          \"site-vpn-flavor\":\"site-vpn-flavor-single\",\r\n          \"management\":{  \r\n            \"type\":\"customer-managed\"\r\n          },\r\n          \"site-network-accesses\":{  \r\n            \"site-network-access\":[  \r\n              {  \r\n                \"site-network-access-id\":\"CE31 to SFO-PE\",\r\n                \"site-network-access-type\":\"multipoint\",\r\n                \"vpn-attachment\":{  \r\n                  \"vpn-id\":\"frinxVPN\",\r\n                  \"site-role\":\"any-to-any-role\"\r\n                },\r\n                \"routing-protocols\":{  \r\n                  \"routing-protocol\":[  \r\n                    {  \r\n                      \"type\":\"bgp\",\r\n                      \"bgp\":{  \r\n                        \"autonomous-system\":65131,\r\n                        \"address-family\":[  \r\n                          \"ipv4\"\r\n                        ]\r\n                      }\r\n                    }\r\n                  ]\r\n                },\r\n                \"ip-connection\":{  \r\n                  \"ipv4\":{  \r\n                    \"address-allocation-type\":\"static-address\",\r\n                    \"addresses\":{  \r\n                      \"provider-address\":\"10.133.131.1\",\r\n                      \"customer-address\":\"10.133.131.10\",\r\n                      \"mask\":24\r\n                    }\r\n                  }\r\n                },\r\n                \"l3vpn-param:pe-node-id\":\"sfo\",\r\n                \"l3vpn-param:pe-2-ce-tp-id\":\"GigabitEthernet0/0/0/3\",\r\n                \"l3vpn-param:pe-bgp-as\":65000\r\n              }\r\n            ]\r\n          }\r\n        },\r\n        {  \r\n          \"site-id\":\"CE32\",\r\n          \"site-vpn-flavor\":\"site-vpn-flavor-single\",\r\n          \"management\":{  \r\n            \"type\":\"customer-managed\"\r\n          },\r\n          \"site-network-accesses\":{  \r\n            \"site-network-access\":[  \r\n              {  \r\n                \"site-network-access-id\":\"CE32 to SYDNEY-PE\",\r\n                \"site-network-access-type\":\"multipoint\",\r\n                \"vpn-attachment\":{  \r\n                  \"vpn-id\":\"frinxVPN\",\r\n                  \"site-role\":\"any-to-any-role\"\r\n                },\r\n                \"routing-protocols\":{  \r\n                  \"routing-protocol\":[  \r\n                    {  \r\n                      \"type\":\"bgp\",\r\n                      \"bgp\":{  \r\n                        \"autonomous-system\":65132,\r\n                        \"address-family\":[  \r\n                          \"ipv4\"\r\n                        ]\r\n                      }\r\n                    }\r\n                  ]\r\n                },\r\n                \"ip-connection\":{  \r\n                  \"ipv4\":{  \r\n                    \"address-allocation-type\":\"static-address\",\r\n                    \"addresses\":{  \r\n                      \"provider-address\":\"10.133.132.1\",\r\n                      \"customer-address\":\"10.133.132.10\",\r\n                      \"mask\":24\r\n                    }\r\n                  }\r\n                },\r\n                \"l3vpn-param:pe-node-id\":\"sydney\",\r\n                \"l3vpn-param:pe-2-ce-tp-id\":\"GigabitEthernet0/0/0/3\",\r\n                \"l3vpn-param:pe-bgp-as\":65000\r\n              }\r\n            ]\r\n          }\r\n        }\r\n      ]\r\n    }\r\n  }\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "create vpn-service cus1_vpn1",
                        "request": {
                            "auth": {
                                "type": "basic",
                                "basic": {
                                    "username": "admin",
                                    "password": "admin",
                                    "saveHelperData": true,
                                    "showPassword": false
                                }
                            },
                            "url": "http://{{odl_ip}}:8181/restconf/config/ietf-l3vpn-svc:l3vpn-svc/vpn-services/vpn-service/cus1_vpn1",
                            "method": "PUT",
                            "header": [
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                },
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{  \r\n  \"vpn-service\":[  \r\n    {  \r\n      \"vpn-id\":\"cus1_vpn1\",\r\n      \"customer-name\":\"customer1\",\r\n      \"vpn-service-topology\":\"any-to-any\",\r\n      \"l3vpn-param:vrf-name\":\"cus1_vpn1\",\r\n      \"l3vpn-param:route-distinguisher\":{  \r\n        \"as\":11,\r\n        \"as-index\":11\r\n      },\r\n      \"l3vpn-param:import-route-targets\":{  \r\n        \"route-target\":{  \r\n          \"as\":11,\r\n          \"as-index\":11\r\n        }\r\n      },\r\n      \"l3vpn-param:export-route-targets\":{  \r\n        \"route-target\":{  \r\n          \"as\":11,\r\n          \"as-index\":11\r\n        }\r\n      }\r\n    }\r\n  ]\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "create site cus1_ce1",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/ietf-l3vpn-svc:l3vpn-svc/sites/site/cus1_ce1",
                            "method": "PUT",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{  \r\n  \"site\":[  \r\n    {  \r\n      \"site-id\":\"cus1_ce1\",\r\n      \"site-vpn-flavor\":\"site-vpn-flavor-single\",\r\n      \"management\":{  \r\n        \"type\":\"customer-managed\"\r\n      },\r\n      \"site-network-accesses\":{  \r\n        \"site-network-access\":[  \r\n          {  \r\n            \"site-network-access-id\":\"cus1_ce1-pe1\",\r\n            \"site-network-access-type\":\"multipoint\",\r\n            \"vpn-attachment\":{  \r\n              \"vpn-id\":\"cus1_vpn1\",\r\n              \"site-role\":\"any-to-any-role\"\r\n            },\r\n            \"routing-protocols\":{  \r\n              \"routing-protocol\":[  \r\n                {  \r\n                  \"type\":\"bgp\",\r\n                  \"bgp\":{  \r\n                    \"autonomous-system\":65101,\r\n                    \"address-family\":[  \r\n                      \"ipv4\"\r\n                    ]\r\n                  }\r\n                }\r\n              ]\r\n            },\r\n            \"ip-connection\":{  \r\n              \"ipv4\":{  \r\n                \"address-allocation-type\":\"static-address\",\r\n                \"addresses\":{  \r\n                  \"provider-address\":\"10.1.11.1\",\r\n                  \"customer-address\":\"10.1.11.10\",\r\n                  \"mask\":24\r\n                }\r\n              }\r\n            },\r\n            \"l3vpn-param:pe-node-id\":\"pe1\",\r\n            \"l3vpn-param:pe-2-ce-tp-id\":\"GigabitEthernet0/0/0/3\",\r\n            \"l3vpn-param:pe-bgp-as\":65000,\r\n            \"l3vpn-param:route-policy-in\":\"RPL_PASS_ALL\",\r\n            \"l3vpn-param:route-policy-out\":\"RPL_PASS_ALL\"\r\n          }\r\n        ]\r\n      }\r\n    }\r\n  ]\r\n}"
                            },
                            "description": "variables:\n\"vpn-id\":\"vpnA\"\n\"customer-name\":\"frinx\"\n\nconstants:\n\"vpn-service-topology\":\"any-to-any\""
                        },
                        "response": []
                    },
                    {
                        "name": "create site cus1_ce2",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/ietf-l3vpn-svc:l3vpn-svc/sites/site/cus1_ce2",
                            "method": "PUT",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{  \r\n  \"site\":[  \r\n    {  \r\n      \"site-id\":\"cus1_ce2\",\r\n      \"site-vpn-flavor\":\"site-vpn-flavor-single\",\r\n      \"management\":{  \r\n        \"type\":\"customer-managed\"\r\n      },\r\n      \"site-network-accesses\":{  \r\n        \"site-network-access\":[  \r\n          {  \r\n            \"site-network-access-id\":\"cus1_ce2-pe2\",\r\n            \"site-network-access-type\":\"multipoint\",\r\n            \"vpn-attachment\":{  \r\n              \"vpn-id\":\"cus1_vpn1\",\r\n              \"site-role\":\"any-to-any-role\"\r\n            },\r\n            \"routing-protocols\":{  \r\n              \"routing-protocol\":[  \r\n                {  \r\n                  \"type\":\"bgp\",\r\n                  \"bgp\":{  \r\n                    \"autonomous-system\":65102,\r\n                    \"address-family\":[  \r\n                      \"ipv4\"\r\n                    ]\r\n                  }\r\n                }\r\n              ]\r\n            },\r\n            \"ip-connection\":{  \r\n              \"ipv4\":{  \r\n                \"address-allocation-type\":\"static-address\",\r\n                \"addresses\":{  \r\n                  \"provider-address\":\"10.1.22.1\",\r\n                  \"customer-address\":\"10.1.22.10\",\r\n                  \"mask\":24\r\n                }\r\n              }\r\n            },\r\n            \"l3vpn-param:pe-node-id\":\"pe2\",\r\n            \"l3vpn-param:pe-2-ce-tp-id\":\"GigabitEthernet0/0/0/3\",\r\n            \"l3vpn-param:pe-bgp-as\":65000,\r\n            \"l3vpn-param:route-policy-in\":\"RPL_PASS_ALL\",\r\n            \"l3vpn-param:route-policy-out\":\"RPL_PASS_ALL\"\r\n          }\r\n        ]\r\n      }\r\n    }\r\n  ]\r\n}"
                            },
                            "description": "variables:\n\"vpn-id\":\"vpnA\"\n\"customer-name\":\"frinx\"\n\nconstants:\n\"vpn-service-topology\":\"any-to-any\""
                        },
                        "response": []
                    },
                    {
                        "name": "delete vpn-service cus1_vpn1",
                        "request": {
                            "auth": {
                                "type": "basic",
                                "basic": {
                                    "username": "admin",
                                    "password": "admin",
                                    "saveHelperData": true,
                                    "showPassword": false
                                }
                            },
                            "url": "http://{{odl_ip}}:8181/restconf/config/ietf-l3vpn-svc:l3vpn-svc/vpn-services/vpn-service/cus1_vpn1",
                            "method": "DELETE",
                            "header": [
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                },
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                        "name": "delete site cus1_ce1",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/ietf-l3vpn-svc:l3vpn-svc/sites/site/cus1_ce1",
                            "method": "DELETE",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": ""
                            },
                            "description": "variables:\n\"vpn-id\":\"vpnA\"\n\"customer-name\":\"frinx\"\n\nconstants:\n\"vpn-service-topology\":\"any-to-any\""
                        },
                        "response": []
                    },
                    {
                        "name": "delete site cus1_ce2",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/ietf-l3vpn-svc:l3vpn-svc/sites/site/cus1_ce2",
                            "method": "DELETE",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": ""
                            },
                            "description": "variables:\n\"vpn-id\":\"vpnA\"\n\"customer-name\":\"frinx\"\n\nconstants:\n\"vpn-service-topology\":\"any-to-any\""
                        },
                        "response": []
                    },
                    {
                        "name": "RPC commit-l3vpn-svc",
                        "request": {
                            "auth": {
                                "type": "basic",
                                "basic": {
                                    "username": "admin",
                                    "password": "admin",
                                    "saveHelperData": true,
                                    "showPassword": false
                                }
                            },
                            "url": "http://{{odl_ip}}:8181/restconf/operations/ietf-l3vpn-svc:commit-l3vpn-svc",
                            "method": "POST",
                            "header": [
                                {
                                    "key": "Cache-Contro",
                                    "value": "no-cache",
                                    "description": ""
                                },
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Accept",
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
                        "name": "status-l3vpn-provider",
                        "request": {
                            "auth": {
                                "type": "basic",
                                "basic": {
                                    "username": "admin",
                                    "password": "admin",
                                    "saveHelperData": true,
                                    "showPassword": false
                                }
                            },
                            "url": "http://{{odl_ip}}:8181/restconf/operational/ietf-l3vpn-svc:status-l3vpn-provider",
                            "method": "GET",
                            "header": [
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                },
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{  \r\n  \"l3vpn-svc\":{  \r\n    \"vpn-services\":{  \r\n      \"vpn-service\":[  \r\n        {  \r\n          \"vpn-id\":\"frinxVPN\",\r\n          \"customer-name\":\"frinx\",\r\n          \"vpn-service-topology\":\"any-to-any\",\r\n          \"l3vpn-param:vrf-name\":\"vrf-CE3\",\r\n          \"l3vpn-param:route-distinguisher\":{  \r\n            \"as\":3,\r\n            \"as-index\":3\r\n          },\r\n          \"l3vpn-param:import-route-targets\":{  \r\n            \"route-target\":{  \r\n              \"as\":3,\r\n              \"as-index\":3\r\n            }\r\n          },\r\n          \"l3vpn-param:export-route-targets\":{  \r\n            \"route-target\":{  \r\n              \"as\":3,\r\n              \"as-index\":3\r\n            }\r\n          }\r\n        }\r\n      ]\r\n    },\r\n    \"sites\":{  \r\n      \"site\":[  \r\n        {  \r\n          \"site-id\":\"CE31\",\r\n          \"site-vpn-flavor\":\"site-vpn-flavor-single\",\r\n          \"management\":{  \r\n            \"type\":\"customer-managed\"\r\n          },\r\n          \"site-network-accesses\":{  \r\n            \"site-network-access\":[  \r\n              {  \r\n                \"site-network-access-id\":\"CE31 to SFO-PE\",\r\n                \"site-network-access-type\":\"multipoint\",\r\n                \"vpn-attachment\":{  \r\n                  \"vpn-id\":\"frinxVPN\",\r\n                  \"site-role\":\"any-to-any-role\"\r\n                },\r\n                \"routing-protocols\":{  \r\n                  \"routing-protocol\":[  \r\n                    {  \r\n                      \"type\":\"bgp\",\r\n                      \"bgp\":{  \r\n                        \"autonomous-system\":65131,\r\n                        \"address-family\":[  \r\n                          \"ipv4\"\r\n                        ]\r\n                      }\r\n                    }\r\n                  ]\r\n                },\r\n                \"ip-connection\":{  \r\n                  \"ipv4\":{  \r\n                    \"address-allocation-type\":\"static-address\",\r\n                    \"addresses\":{  \r\n                      \"provider-address\":\"10.133.131.1\",\r\n                      \"customer-address\":\"10.133.131.10\",\r\n                      \"mask\":24\r\n                    }\r\n                  }\r\n                },\r\n                \"l3vpn-param:pe-node-id\":\"sfo\",\r\n                \"l3vpn-param:pe-2-ce-tp-id\":\"GigabitEthernet0/0/0/3\",\r\n                \"l3vpn-param:pe-bgp-as\":65000\r\n              }\r\n            ]\r\n          }\r\n        },\r\n        {  \r\n          \"site-id\":\"CE32\",\r\n          \"site-vpn-flavor\":\"site-vpn-flavor-single\",\r\n          \"management\":{  \r\n            \"type\":\"customer-managed\"\r\n          },\r\n          \"site-network-accesses\":{  \r\n            \"site-network-access\":[  \r\n              {  \r\n                \"site-network-access-id\":\"CE32 to SYDNEY-PE\",\r\n                \"site-network-access-type\":\"multipoint\",\r\n                \"vpn-attachment\":{  \r\n                  \"vpn-id\":\"frinxVPN\",\r\n                  \"site-role\":\"any-to-any-role\"\r\n                },\r\n                \"routing-protocols\":{  \r\n                  \"routing-protocol\":[  \r\n                    {  \r\n                      \"type\":\"bgp\",\r\n                      \"bgp\":{  \r\n                        \"autonomous-system\":65132,\r\n                        \"address-family\":[  \r\n                          \"ipv4\"\r\n                        ]\r\n                      }\r\n                    }\r\n                  ]\r\n                },\r\n                \"ip-connection\":{  \r\n                  \"ipv4\":{  \r\n                    \"address-allocation-type\":\"static-address\",\r\n                    \"addresses\":{  \r\n                      \"provider-address\":\"10.133.132.1\",\r\n                      \"customer-address\":\"10.133.132.10\",\r\n                      \"mask\":24\r\n                    }\r\n                  }\r\n                },\r\n                \"l3vpn-param:pe-node-id\":\"sydney\",\r\n                \"l3vpn-param:pe-2-ce-tp-id\":\"GigabitEthernet0/0/0/3\",\r\n                \"l3vpn-param:pe-bgp-as\":65000\r\n              }\r\n            ]\r\n          }\r\n        }\r\n      ]\r\n    }\r\n  }\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "configured-l3vpn",
                        "request": {
                            "auth": {
                                "type": "basic",
                                "basic": {
                                    "username": "admin",
                                    "password": "admin",
                                    "saveHelperData": true,
                                    "showPassword": false
                                }
                            },
                            "url": "http://{{odl_ip}}:8181/restconf/operational/ietf-l3vpn-svc:configured-l3vpn-svc",
                            "method": "GET",
                            "header": [
                                {
                                    "key": "Content-Type",
                                    "value": "application/json",
                                    "description": ""
                                },
                                {
                                    "key": "Cache-Control",
                                    "value": "no-cache",
                                    "description": ""
                                },
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{  \r\n  \"l3vpn-svc\":{  \r\n    \"vpn-services\":{  \r\n      \"vpn-service\":[  \r\n        {  \r\n          \"vpn-id\":\"frinxVPN\",\r\n          \"customer-name\":\"frinx\",\r\n          \"vpn-service-topology\":\"any-to-any\",\r\n          \"l3vpn-param:vrf-name\":\"vrf-CE3\",\r\n          \"l3vpn-param:route-distinguisher\":{  \r\n            \"as\":3,\r\n            \"as-index\":3\r\n          },\r\n          \"l3vpn-param:import-route-targets\":{  \r\n            \"route-target\":{  \r\n              \"as\":3,\r\n              \"as-index\":3\r\n            }\r\n          },\r\n          \"l3vpn-param:export-route-targets\":{  \r\n            \"route-target\":{  \r\n              \"as\":3,\r\n              \"as-index\":3\r\n            }\r\n          }\r\n        }\r\n      ]\r\n    },\r\n    \"sites\":{  \r\n      \"site\":[  \r\n        {  \r\n          \"site-id\":\"CE31\",\r\n          \"site-vpn-flavor\":\"site-vpn-flavor-single\",\r\n          \"management\":{  \r\n            \"type\":\"customer-managed\"\r\n          },\r\n          \"site-network-accesses\":{  \r\n            \"site-network-access\":[  \r\n              {  \r\n                \"site-network-access-id\":\"CE31 to SFO-PE\",\r\n                \"site-network-access-type\":\"multipoint\",\r\n                \"vpn-attachment\":{  \r\n                  \"vpn-id\":\"frinxVPN\",\r\n                  \"site-role\":\"any-to-any-role\"\r\n                },\r\n                \"routing-protocols\":{  \r\n                  \"routing-protocol\":[  \r\n                    {  \r\n                      \"type\":\"bgp\",\r\n                      \"bgp\":{  \r\n                        \"autonomous-system\":65131,\r\n                        \"address-family\":[  \r\n                          \"ipv4\"\r\n                        ]\r\n                      }\r\n                    }\r\n                  ]\r\n                },\r\n                \"ip-connection\":{  \r\n                  \"ipv4\":{  \r\n                    \"address-allocation-type\":\"static-address\",\r\n                    \"addresses\":{  \r\n                      \"provider-address\":\"10.133.131.1\",\r\n                      \"customer-address\":\"10.133.131.10\",\r\n                      \"mask\":24\r\n                    }\r\n                  }\r\n                },\r\n                \"l3vpn-param:pe-node-id\":\"sfo\",\r\n                \"l3vpn-param:pe-2-ce-tp-id\":\"GigabitEthernet0/0/0/3\",\r\n                \"l3vpn-param:pe-bgp-as\":65000\r\n              }\r\n            ]\r\n          }\r\n        },\r\n        {  \r\n          \"site-id\":\"CE32\",\r\n          \"site-vpn-flavor\":\"site-vpn-flavor-single\",\r\n          \"management\":{  \r\n            \"type\":\"customer-managed\"\r\n          },\r\n          \"site-network-accesses\":{  \r\n            \"site-network-access\":[  \r\n              {  \r\n                \"site-network-access-id\":\"CE32 to SYDNEY-PE\",\r\n                \"site-network-access-type\":\"multipoint\",\r\n                \"vpn-attachment\":{  \r\n                  \"vpn-id\":\"frinxVPN\",\r\n                  \"site-role\":\"any-to-any-role\"\r\n                },\r\n                \"routing-protocols\":{  \r\n                  \"routing-protocol\":[  \r\n                    {  \r\n                      \"type\":\"bgp\",\r\n                      \"bgp\":{  \r\n                        \"autonomous-system\":65132,\r\n                        \"address-family\":[  \r\n                          \"ipv4\"\r\n                        ]\r\n                      }\r\n                    }\r\n                  ]\r\n                },\r\n                \"ip-connection\":{  \r\n                  \"ipv4\":{  \r\n                    \"address-allocation-type\":\"static-address\",\r\n                    \"addresses\":{  \r\n                      \"provider-address\":\"10.133.132.1\",\r\n                      \"customer-address\":\"10.133.132.10\",\r\n                      \"mask\":24\r\n                    }\r\n                  }\r\n                },\r\n                \"l3vpn-param:pe-node-id\":\"sydney\",\r\n                \"l3vpn-param:pe-2-ce-tp-id\":\"GigabitEthernet0/0/0/3\",\r\n                \"l3vpn-param:pe-bgp-as\":65000\r\n              }\r\n            ]\r\n          }\r\n        }\r\n      ]\r\n    }\r\n  }\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "provider-edge-topology OPER",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/operational/network-topology:network-topology/topology/provider-edge-topology",
                            "method": "GET",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Accept",
                                    "value": "application/yang.data+json",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{\r\n  \"input\":{\r\n  }\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    }
                ]
            },
            {
                "name": "fictive network element connection",
                "description": "",
                "item": [
                    {
                        "name": "connect pe1",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/mock-pe-topology/node/pe1",
                            "method": "PUT",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                                "raw": "{\n  \"node\": [\n    {\n      \"node-id\": \"pe1\",\n      \"termination-point\": [\n        {\n          \"tp-id\":\"GigabitEthernet0/0/0/1\"\n        },\n        {\n          \"tp-id\":\"GigabitEthernet0/0/0/2\"\n        },\n        {\n          \"tp-id\":\"GigabitEthernet0/0/0/3\"\n        }\n      ]\n    }\n  ]\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "connect pe2",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/mock-pe-topology/node/pe2",
                            "method": "PUT",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                                "raw": "{\n  \"node\": [\n    {\n      \"node-id\": \"pe2\",\n      \"termination-point\": [\n        {\n          \"tp-id\":\"GigabitEthernet0/0/0/1\"\n        },\n        {\n          \"tp-id\":\"GigabitEthernet0/0/0/2\"\n        },\n        {\n          \"tp-id\":\"GigabitEthernet0/0/0/3\"\n        }\n      ]\n    }\n  ]\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "nodes OPER",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/operational/network-topology:network-topology/topology/mock-pe-topology",
                            "method": "GET",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Accept",
                                    "value": "application/yang.data+json",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{\r\n  \"input\":{\r\n  }\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "nodes CONF",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/mock-pe-topology",
                            "method": "GET",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
                                    "description": ""
                                },
                                {
                                    "key": "Accept",
                                    "value": "application/yang.data+json",
                                    "description": ""
                                }
                            ],
                            "body": {
                                "mode": "raw",
                                "raw": "{\r\n  \"input\":{\r\n  }\r\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "disconnect pe1",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/mock-pe-topology/node/pe1",
                            "method": "DELETE",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                                "raw": "{\n  \"node\": [\n    {\n      \"node-id\": {{router_name}},\n      \"netconf-node-topology:host\": {{router_ip}},\n      \"netconf-node-topology:port\": 830,\n      \"netconf-node-topology:keepalive-delay\": 0,\n      \"netconf-node-topology:tcp-only\": false,\n      \"netconf-node-topology:username\": \"cisco\",\n      \"netconf-node-topology:password\": \"cisco\"\n    }\n  ]\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    },
                    {
                        "name": "disconnect pe2",
                        "request": {
                            "url": "http://{{odl_ip}}:8181/restconf/config/network-topology:network-topology/topology/mock-pe-topology/node/pe2",
                            "method": "DELETE",
                            "header": [
                                {
                                    "key": "Authorization",
                                    "value": "Basic YWRtaW46YWRtaW4=",
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
                                "raw": "{\n  \"node\": [\n    {\n      \"node-id\": {{router_name}},\n      \"netconf-node-topology:host\": {{router_ip}},\n      \"netconf-node-topology:port\": 830,\n      \"netconf-node-topology:keepalive-delay\": 0,\n      \"netconf-node-topology:tcp-only\": false,\n      \"netconf-node-topology:username\": \"cisco\",\n      \"netconf-node-topology:password\": \"cisco\"\n    }\n  ]\n}"
                            },
                            "description": ""
                        },
                        "response": []
                    }
                ]
            }
        ]
    }