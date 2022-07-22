# ansible-role-k8s-rke

[![Ansible Role](https://img.shields.io/ansible/quality/27842.svg)](https://galaxy.ansible.com/isweluiz/ansible_role_k8s_rke)
[![License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](https://github.com/isweluiz/ansible-package-debian-manage/blob/master/LICENSE)

## Ansible Role: ansible-role-k8s-rke 

An ansible role that setup kubernetes cluster with rke on rhel/centos/fedora and debian/ubuntu. 

## Dependencies: 

Docker - You can use the [ansible-role-docker](https://github.com/geerlingguy/ansible-role-docker)
Kubectl - To manager the k8s cluster [anisble-role-kubectl](https://github.com/githubixx/ansible-role-kubectl)

## Variables:

* `rke_kubernetes_version`: `v1.23.6-rancher1-1` - Map the RKE kubernetes image version across the selection to the kubernetes version.

* `rke_version`: `v1.2.1` - Defines rke version.


* `rke_binary_url`: `"https://github.com/rancher/rke/releases/download/{{ rke_version }}/rke_linux-amd64"` - Defines rke binary url download.


* `rke_user`: `rke` - User that will be used to connect on nodes during the installation proccess.


* `rke_node`: `"{{ groups['masters'] | first }}"` - Node that will be used to deploy cluster using RKE.


* `rke_cluster_network_cidr`: `'10.42.0.0/16'` - CIDR pool used to assign IP addresses to pods in the cluster.


* `rke_service_network_cidr`: `'10.43.0.0/16'` - This is the virtual IP address that will be assigned to services created on Kubernetes.

## Playbook Example: 

```yaml
---
- name: "Deploy :: RKE k8s cluster" 
  hosts: k8s
  tasks: 
    - name: "Include rke Role"
      include_role:
        name: ansible-rke-k8s 
...
```

## Inventory 

```yaml
############# GROUPS #############
[k8s:children]
masters
etcd
workers

[etcd:children]
masters

[workers:children]
masters
workers_nodes

[masters]
node1
node2 
node3

[workers_nodes]
node4
node5
node6
node7
```

License
-------

MIT

Author Information
------------------
- [Ansible Galaxy](https://galaxy.ansible.com/isweluiz)
- [Github](https://github.com/isweluiz)
- [Linkedin](https://www.linkedin.com/in/isweluiz)