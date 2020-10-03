# Provisioning Pod Network Routes

Pods scheduled to a node receive an IP address from the node's Pod CIDR range. At this point pods can not communicate with other pods running on different nodes due to missing network [routes](https://cloud.google.com/compute/docs/vpc/routes).

In this lab you will create a route for each worker node that maps the node's Pod CIDR range to the node's internal IP address.

> There are [other ways](https://kubernetes.io/docs/concepts/cluster-administration/networking/#how-to-achieve-this) to implement the Kubernetes networking model.

## Routes

Create network routes for each worker instance:
> route add -net <WORKER_POD_CIDR> netmask 255.255.255.0 gw <WORKER_IP>

```
route add -net 10.234.64.0 netmask 255.255.255.0 gw 10.2.35.4
route add -net 10.234.65.0 netmask 255.255.255.0 gw 10.2.35.5
route add -net 10.234.66.0 netmask 255.255.255.0 gw 10.2.35.6
```

List the routes in the network:

```
ip route show
```

Next: [Deploying the DNS Cluster Add-on](12-dns-addon.md)
