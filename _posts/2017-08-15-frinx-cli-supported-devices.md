---
ID: 5518
post_title: FRINX CLI supported devices
author: frinxadmin
post_excerpt: ""
layout: post
permalink: >
  https://frinx.io/frinx-feature-guide/frinx-cli-supported-devices.html
published: true
post_date: 2017-08-15 14:16:13
---
    {
        "available-cli-device-translations": {
            "available-cli-device-translation": [
                {
                    "device-type": "ios",
                    "device-version": "*",
                    "units": {
                        "unit": [
                            {
                                "id": "IOS basic translate unit",
                                "models": {
                                    "model": [
                                        {
                                            "id": "urn:opendaylight:params:xml:ns:yang:ios:essential?module=ios-essential&;revision=2017-05-20",
                                            "implemented-readers": [
                                                "/version",
                                                "/vrfs/vrf"
                                            ],
                                            "implemented-writers": [
                                                "/vrfs/vrf"
                                            ]
                                        }
                                    ]
                                }
                            },
                            {
                                "id": "IOS Interface (Openconfig) translate unit",
                                "models": {
                                    "model": [
                                        {
                                            "id": "http://openconfig.net/yang/interfaces/ip?module=openconfig-if-ip&;revision=2016-12-22",
                                            "implemented-readers": [
                                                "/interfaces/interface/subinterfaces/subinterface/ipv4/addresses/address/config",
                                                "/interfaces/interface/subinterfaces/subinterface/ipv4/addresses/address"
                                            ],
                                            "implemented-writers": [
                                                "/interfaces/interface/subinterfaces/subinterface/ipv4/addresses/address/config",
                                                "/interfaces/interface/subinterfaces/subinterface/ipv4/addresses/address"
                                            ]
                                        },
                                        {
                                            "id": "urn:ietf:params:xml:ns:yang:ietf-interfaces?module=ietf-interfaces&;revision=2014-05-08"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/vlan-types?module=openconfig-vlan-types&;revision=2016-05-26"
                                        },
                                        {
                                            "id": "urn:ietf:params:xml:ns:yang:ietf-inet-types?module=ietf-inet-types&;revision=2013-07-15"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/openconfig-ext?module=openconfig-extensions&;revision=2017-01-29"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/interfaces/ethernet?module=openconfig-if-ethernet&;revision=2016-12-22"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/interfaces?module=openconfig-interfaces&;revision=2016-12-22",
                                            "implemented-readers": [
                                                "/interfaces/interface/config",
                                                "/interfaces/interface/subinterfaces/subinterface",
                                                "/interfaces/interface",
                                                "/interfaces/interface/state"
                                            ],
                                            "implemented-writers": [
                                                "/interfaces/interface/subinterfaces/subinterface",
                                                "/interfaces/interface",
                                                "/interfaces/interface/config"
                                            ]
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/interfaces/aggregate?module=openconfig-if-aggregate&;revision=2016-12-22"
                                        },
                                        {
                                            "id": "urn:ietf:params:xml:ns:yang:iana-if-type?module=iana-if-type&;revision=2014-05-08"
                                        },
                                        {
                                            "id": "urn:ietf:params:xml:ns:yang:ietf-yang-types?module=ietf-yang-types&;revision=2013-07-15"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/vlan?module=openconfig-vlan&;revision=2016-05-26"
                                        }
                                    ]
                                }
                            },
                            {
                                "id": "ios-bgp-unit",
                                "models": {
                                    "model": [
                                        {
                                            "id": "http://openconfig.net/yang/rib/bgp?module=openconfig-rib-bgp&;revision=2016-10-17",
                                            "implemented-readers": [
                                                "/bgp-rib"
                                            ]
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/bgp?module=openconfig-bgp&;revision=2017-02-02",
                                            "implemented-readers": [
                                                "/bgp"
                                            ]
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/rib/bgp?module=openconfig-rib-bgp-shared-attributes&;revision=2016-10-17"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/rib/bgp-types?module=openconfig-rib-bgp-types&;revision=2016-10-17"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/bgp-types?module=openconfig-bgp-types&;revision=2017-02-02"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/openconfig-types?module=openconfig-types&;revision=2017-01-13"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/types/inet?module=openconfig-inet-types&;revision=2017-04-03"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/rib/bgp?module=openconfig-rib-bgp-attributes&;revision=2016-10-17"
                                        },
                                        {
                                            "id": "urn:ietf:params:xml:ns:yang:ietf-yang-types?module=ietf-yang-types&;revision=2013-07-15"
                                        },
                                        {
                                            "id": "urn:ietf:params:xml:ns:yang:ietf-interfaces?module=ietf-interfaces&;revision=2014-05-08"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/policy-types?module=openconfig-policy-types&;revision=2016-05-12"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/bgp?module=openconfig-bgp-common-multiprotocol&;revision=2017-02-02"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/rib/bgp?module=openconfig-rib-bgp-tables&;revision=2016-10-17"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/rib/bgp?module=openconfig-rib-bgp-table-attributes&;revision=2016-10-17"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/bgp?module=openconfig-bgp-neighbor&;revision=2017-02-02"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/bgp?module=openconfig-bgp-peer-group&;revision=2017-02-02"
                                        },
                                        {
                                            "id": "urn:ietf:params:xml:ns:yang:ietf-inet-types?module=ietf-inet-types&;revision=2013-07-15"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/types/yang?module=openconfig-yang-types&;revision=2017-04-03"
                                        },
                                        {
                                            "id": "urn:opendaylight:params:xml:ns:yang:ios:bgp?module=ios-bgp-unit&;revision=2017-06-10"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/bgp?module=openconfig-bgp-common&;revision=2017-02-02"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/bgp?module=openconfig-bgp-global&;revision=2017-02-02"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/openconfig-ext?module=openconfig-extensions&;revision=2017-01-29"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/interfaces?module=openconfig-interfaces&;revision=2016-12-22"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/bgp?module=openconfig-bgp-common-structure&;revision=2017-02-02"
                                        },
                                        {
                                            "id": "http://openconfig.net/yang/routing-policy?module=openconfig-routing-policy&;revision=2016-05-12"
                                        }
                                    ]
                                }
                            }
                        ]
                    }
                },
                {
                    "device-type": "*",
                    "device-version": "*",
                    "units": {
                        "unit": [
                            {
                                "id": "Baseline translate unit",
                                "models": {
                                    "model": [
                                        {
                                            "id": "urn:opendaylight:params:xml:ns:yang:cli:unit:generic?module=cli-unit-generic&;revision=2017-05-20",
                                            "implemented-rpcs": [
                                                "execute",
                                                "execute-and-read-until",
                                                "execute-and-read"
                                            ]
                                        }
                                    ]
                                }
                            }
                        ]
                    }
                }
            ]
        }
    }