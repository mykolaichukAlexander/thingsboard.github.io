#### Azure Kubernetes Service (AKS)

For AKS if you have all needed permissions , after filling all parameters, Kubernetes cluster should create all needed resources.

| Name                            |                Description                 |      Default Value |
|---------------------------------|:------------------------------------------:|-------------------:|
| azure.loadBalancer.enabled      |      Enable AKS Ingress Load Balancer      |              false |
| azure.loadBalancer.cert.enabled |   Enable AKS Ingress Load Balancer HTTPS   |              false |
| azure.loadBalancer.cert.secret  | Secret name that contains your certificate |          akssecret |
| hosts.loadBalancer.cert.hosts   |    List hosts that will use in ingress     | ["www.exaple.com"] |


> **_NOTE:_** For creation secret from cert and key file you can use:
>```shell
>kubectl create secret tls my-tls-secret \
>  --cert=path/to/cert/file \
>  --key=path/to/key/file
>```
