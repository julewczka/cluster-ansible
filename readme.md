# Initialize K8s cluster with Ansible with 3 vm's

The project contains ansible playbooks, which will initialize a Kubernetes cluster by running 

`ansible-playbook -i inventory.yaml site.yaml --ask-become-pass`

## Prerequisites

In order to run above command succesfully, you need 3 virtual machines with following packages installed:

- python3

In Addition you need to install following packages on the host (ansible controller machine):

- ansible 
- kubernetes.core module for ansible

Kubernetes.core module can be installed with `ansible-galaxy collection install kubernetes.core`.

and following minimum requirements ([K8s hw recommendation](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)) for virtual hardware:

- atleast 2 cpu cores on your host
- atleast 2G of memory per machine 

The playbook was tested for vm's based on Ubuntu 22.04. with:
- 2 cpu cores & 4G of memory for control plane
- 1 cpu & 4G of memory per workers

Make sure to enable ssh connections between host (Ansible controller machine) and remote nodes by adding public key to each node.

## Container runtime

Containerd is installed as container runtime engine for this setup. 

## Network addon

[Weave Net](https://www.weave.works/docs/net/latest/kubernetes/kube-addon/) addon is being used as network plugin for K8s. You can choose another network policy provider by replacing the daemonset in `roles/control-plane/files/`.
