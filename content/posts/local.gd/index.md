---
title: "Local.gd"
date: 2022-09-22T16:50:15+02:00
tags: [network, homelab, dns]
summary: >-
    The easiest way to serve localhost. DNS that always resolves to 127.0.0.1.
---

## What is

[Local.gd](https://local.gd/) is a service that resolve every url as `127.0.0.1`.  
Use **mysite.local.gd** when developing locally and it'll resolve to **127.0.0.1** just like magic!  
Any subdomain like *.local.gd will work.

This mean if you call `cluster.local.gd` the browser call the 127.0.0.1

This is very usefull when you want test a cluster o services in your machine and dont want change the `/etc/hosts` or install `dnsmasq` service.

## Configuration

There is 0 configuration. Just call the `<name>`.local.gd

🎉 Happy coding