# Provisioning Pod Network Routes

Pods scheduled to a node receive an IP address from the node's Pod CIDR range. At this point pods can not communicate with other pods running on different nodes due to missing network [routes](https://cloud.google.com/compute/docs/vpc/routes).

In this lab you will create a route for each worker node that maps the node's Pod CIDR range to the node's internal IP address.

> There are [other ways](https://kubernetes.io/docs/concepts/cluster-administration/networking/#how-to-achieve-this) to implement the Kubernetes networking model.

We chose to use CNI - [calico](https://github.com/projectcalico/calico) as our networking option.

### Deploy Calico Network - WIP
Use the Kubernetes datastore manifest (recommended by the Calico Project)<br>
Uncomment the CALICO_IPV4POOL_CIDR variable in the manifest and set it to the same value as your chosen pod CIDR.
```
{
  curl https://docs.projectcalico.org/v3.16/manifests/calico.yaml -O
  POD_CIDR="10.234.64.0/18"
  sed -i -e "s?192.168.0.0/16?$POD_CIDR?g" calico.yaml
  sed -i '/CALICO_IPV4POOL_CIDR/s/# //g' calico.yaml
  sed -i '/10.234.64.0/s/# //g' calico.yaml
  kubectl apply -f ./calico.yaml  
}
```

If calico is not starting and you get an error '/var/lib/calico/nodename: no such file or directory' run the following command on all worker nodes then try and redeploy calico.
```
echo $HOSTNAME > /var/lib/calico/nodename
```

Reference: https://docs.projectcalico.org/getting-started/kubernetes/self-managed-onprem/onpremises

## Verification

List the registered Kubernetes nodes from the master node:

```
kubectl get pods -n kube-system
```
Reference: https://kubernetes.io/docs/tasks/administer-cluster/network-policy-provider/calico-network-policy/

Next: [Deploying the DNS Cluster Add-on](12-dns-addon.md)
