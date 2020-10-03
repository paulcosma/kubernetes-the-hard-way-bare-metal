# Provisioning Compute Resources

Kubernetes requires a set of machines to host the Kubernetes control plane and the worker nodes where containers are ultimately run. In this lab you will provision the compute resources required for running a secure and highly available Kubernetes cluster.

- Create 7 VMs with the name 'kube-0*' 
    - 1 Loadbalancer
    - 3 Master 
    - 3 Worker
- Operating System: Ubuntu Server 20.04

## Networking

- Set's IP addresses in the range 10.2.35.0/24

    | VM            |  VM Name   | CPU  | RAM       | IP        |
    | -----------   | ---------  |:----:| :--------:| :--------:|
    | loadbalancer  | kube00     | 1    | 522 MiB   | 10.2.35.0 |
    | master-1      | kube01     | 1    | 2048 MiB  | 10.2.35.1 |
    | master-2      | kube02     | 1    | 2048 MiB  | 10.2.35.2 |
    | master-3      | kube03     | 1    | 2048 MiB  | 10.2.35.3 |
    | worker-1      | kube04     | 1    | 1024 MiB  | 10.2.35.4 |
    | worker-2      | kube05     | 1    | 1024 MiB  | 10.2.35.5 |
    | worker-3      | kube06     | 1    | 1024 MiB  | 10.2.35.6 |   

The Kubernetes [networking model](https://kubernetes.io/docs/concepts/cluster-administration/networking/#kubernetes-model) assumes a flat network in which containers and nodes can communicate with each other. In cases where this is not desired [network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/) can limit how groups of containers are allowed to communicate with each other and external network endpoints.

> Setting up network policies is out of scope for this tutorial.

A subnet must be provisioned with an IP address range large enough to assign a private IP address to each node in the Kubernetes cluster.

> The `10.2.35.0/24` IP address range can host up to 254 compute instances.


- Runs the below command on all nodes to allow for network forwarding in IP Tables.
  This is required for kubernetes networking to function correctly.
    > sysctl net.bridge.bridge-nf-call-iptables=1


## Tools
Install necessary tools on all VMs
```
apt-get install -y net-tools
```

## Configuring SSH Access

SSH will be used to configure the controller(master) and worker instances. Make sure you can access all nodes via SSH.

# Verify Environment
- Ensure all VMs are up
- Ensure VMs are assigned the above IP addresses
- Ensure you can SSH into these VMs using the IP and private keys
- Ensure the VMs can ping each other 

Next: [Provisioning a CA and Generating TLS Certificates](04-certificate-authority.md)
