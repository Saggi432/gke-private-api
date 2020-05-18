# k8s-private-api 

This helm chart lets you to access your k8s api server from your desktop when your api server end point is configured as a private endpoint.


## Objective

Currently there are several ways to access a k8s-api-server configured with private end point on GCP. By deploying this helm chart you should be able to access the k8s api from your desktop as long as you are in your corporate network.



## Prerequisites

- Assume that the VPC is configured with corporate VPN or TRANSIT GW so that you can still access the other compute instances/loadbalancers configured on the VPC
- Helm3 is installed and configured on your cluster
- (Optional) You have a hosted zone configure on Route53, this is not required if you have external-dns configured on your reserver.

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install foobar.

```bash
git clone https://github.com/Saggi432/k8s-private-api.git
cd k8s-private-api
helm install .
```

## Usage

```python
export https_proxy=http://k8s-private-api.<hostedzone>.com
kubectl get pods -v100
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
