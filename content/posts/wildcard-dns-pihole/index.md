---
title: "Wildcard Dns Pihole"
date: 2022-07-15T16:29:30+02:00
tags:
    - network
    - homelab
summary: >-
    How to add custom wildcard dns into Pi-Hole home lab
---

If you're running a homelab you might be running a DNS server, like bind to manage your DNS records, zones, etc, and frankly, bind does an excellent job at that. However, sometime you might find your self running a home lab with a service like Pi-Hole.

With Pi-Hole you can create a custom DNS with a simple click, but you can't create a wildcard DNS via web interface.

## Why a wildcard DNS?
If you plan to run a kubernetes cluster, openshift, traefik or reverse-proxy you need point all subdomain name
into a one ip.

## Create a wildcard DNS
Connect to Pi-Hole machine or container and follow these steps:
1. go to `/etc/dnsmasq.d/`
2. create a new file, lets call it `02-my-wildcard-dns.conf`
3. Edit the file and add this:

    ```txt
    address=/my-wildcard.home/192.168.1.40
    ```

4. Save and exit
5. Restart Pi-Hole service with
    ```bash
    service pihole-FTL restart
    ```

You can add one ore more wilcard dns rule in step 3 as you want.

🎉 Happy dns