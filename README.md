## Overview

This is a simple Ansible playbook to setup a Rook Storage Cluster inside an already available Kubernetes Cluster.

## Pre-Requisites

Node in the `k8s_master` group of the `inventory/hosts.cfg` is the Kubernetes cluster's master node. It's assumed that `kubectl` command is available and setup there for the tasks in the playbook to work. Along with the Kubernetes cluster, Rook Operator also need to be setup in the same cluster as mentioned ![here](https://rook.github.io/docs/rook/master/kubernetes.html)

## Approach & Configuration

The approach to setup Rook Storage cluster in this playbook is that a particular mount point in all the nodes assigned for storage will be used as the storage cluster's directories. This same information is mentioned in the `templates/rook-cluster-config.ymk.j2`.

Along with the Rook cluster, this playbook also sets up Rook Toolbox required to monitor the Rook / Ceph cluster.

The `storage_nodes` in the `inventory/hosts.cfg` denotes the storage node details. Other relvant values for the Rook cluster setup is in the `inventory/group_vars/k8s_master.yml`. The `inventory/group_vars/all/vault.yml` contain some sensitive information like the actual IPs and ssh user, please make sure to edit them before executing the playbook.

For more details check on ![Rook](https://rook.github.io/docs/rook/master/kubernetes.html), ![Rook Cluster setup template](https://rook.github.io/docs/rook/master/cluster-crd.html) and ![Rook toolbox](https://rook.github.io/docs/rook/master/toolbox.html)

## Playbook execution

```
$ ansible-playbook -i inventory/hosts.cfg -kK -v --ask-vault-pass playbook.yml
```
