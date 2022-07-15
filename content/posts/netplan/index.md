---
title: "Netplan"
date: 2022-07-14T16:50:15+02:00
tags: [ubuntu, network, homelab]
summary: >-
    How to configure dhcp or static ip on ubuntu with netplan
---

## Ubuntu netplan

To configure netplan, save configuration files under `/etc/netplan/` with a `.yaml`  
To test and save configuration

```bash
netplan generate
netplan apply
```

## Example
### DCHP

```yaml
network:
    version: 2
    renderer: networkd
    ethernets:
        enp3s0:
            dhcp4: true
```

### Static IP
```yaml
network:
    version: 2
    renderer: networkd
    ethernets:
        enp3s0:
            addresses:
                - 10.10.10.2/24
            nameservers:
                addresses:
                    - 10.10.10.1, 
                    - 1.1.1.1
            routes:
                - to: default
                  via: 10.10.10.1
```

For more example see [Documentation](https://netplan.io/examples/)

🎉 Happy networking