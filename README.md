# k8s-private-api 

This helm chart lets you to access your k8s api server from your desktop when your api server end point is configured as a private endpoint.


## Objective

Currently there are several ways to access a k8s-api-server configured with private end point on GCP. By deploying this helm chart you should be able to access the k8s api from your desktop as long as you are in your corporate network.

The solution is based on the below link, which requires many manual steps of creating a docker image, k8s deployment and network load balancer to access an API servers. By using this helm chart it avoids these manual steps.

https://cloud.google.com/solutions/creating-kubernetes-engine-private-clusters-with-net-proxies

This solution is targetted towards GKE private clusters with no access to public endpoint.

https://cloud.google.com/kubernetes-engine/docs/how-to/private-clusters#private_master


## Prerequisites

- Assume that the VPC is configured with corporate VPN so that you can still access the other compute instances/loadbalancers configured on the VPC once you are in your corporate network.
- Helm3 is installed and configured on your cluster
- You have a hosted zone configure on Route53 so that you can create CNAME with FQDN for the generated load balancer. However if an external-dns is already running on your cluster these changes are not required.


## Installation

Use the package manager helm to install.

```bash

git clone https://github.com/Saggi432/k8s-private-api.git
cd k8s-private-api
helm install . --namespace default --name k8s-private-api --set fqdn=k8s-api-proxy.myhostezone.com

```

## Usage

```python
export LB_IP=`kubectl get  service/k8s-api-proxy \
-o jsonpath='{.status.loadBalancer.ingress[].ip}'`
export https_proxy=$LB_IP:8118
kubectl get pods -v100
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
