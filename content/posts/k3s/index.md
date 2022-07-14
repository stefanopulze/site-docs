---
title: "K3S Lightweight Kubernetes"
date: 2022-07-14T09:10:13+02:00
tags:
- docker
- k8s
- cluster
slug: k3s
summary: >-
    k3s is a single binary lightweight kubernetes service. It can run on any pc, raspberry or in a edge iot device
draft: true
---

## Why k3s

Is a single binary lightweight kubernetes service. It can run on any pc, raspberry or in a edge iot device: it use less memory as possibile to leave more resources for your services.

`Rancher K3S` can be configured as single node cluster or high availability production cluster.

## Install cluster in HA
### Instal master nodes
To have a HA cluster you need almost `3 master` as control panel.

`K3S`, after the release `v1.19.5+k3s1`, came with a embeded etcd cluster service. But if you want you can configure an external DB such as: mysql, postress or etcd.

For this example we use embeded etcd service.

```bash
# First master node
curl -sfL https://get.k3s.io | sh -s - server \
--write-kubeconfig-mode 644 \
--token <my super secret token> \
--cluster-init 
```

After launching the first server, join the second and third servers to the cluster using the shared secret:

```bash
curl -sfL https://get.k3s.io | sh -s - server \
--write-kubeconfig-mode 644 \
--token <my super secret token> \
--server https://<ip or hostname of server1>:6443
```

### Instal aget nodes

```bash
curl -sfL https://get.k3s.io | K3S_TOKEN=<my super secret token> \
K3S_KUBECONFIG_MODE="644" \
K3S_URL=https://<ip or hostname of server1>:6443 sh -
```

### Check nodes status

Run into a node the following command to check nodes
```bash
kubectl get nodes

NAME     STATUS   ROLES                       AGE   VERSION
k3s-01   Ready    control-plane,etcd,master   33m   v1.23.8+k3s2
k3s-02   Ready    control-plane,etcd,master   30m   v1.23.8+k3s2
k3s-03   Ready    control-plane,etcd,master   26m   v1.23.8+k3s2
k3s-04   Ready    <none>                      19s   v1.23.8+k3s2
```

## Export kubectl configuration
In order to connecto to cluster from your computer you need to export the configuration.

K3S save the kubeconfig into `/etc/rancher/k3s/k3s.yaml`. You need to copy the file content and change the server ip with the real IP or name of server.

Then you can connect
```bash
kubectl --kubeconfig ~/kubeconfig.yaml get nodes
```

Your HA cluster is now up and running.

🎉 Happy deploy