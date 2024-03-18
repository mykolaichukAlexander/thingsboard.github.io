#### Google Kubernetes Engine (GKE)

This chart has basic configuration for using Google Kubernetes Engine Controller that described in [docs](https://cloud.google.com/kubernetes-engine/docs/concepts/ingress-xlb).

Before install if you want to Cluster has the same ip even after ingress recreated you need to follow [this doc](https://cloud.google.com/compute/docs/ip-addresses/reserve-static-external-ip-address)
and after put a name into `gcloud.loadBalancer.staticAddressName`.

If you pass `gcloud.loadBalancer.cert.enabled` as true chart will create Google manage certificate. Your domain name should resolve to google load balancer ip otherwise certificate will not be approved.


| Name                                           |                                   Description                                    |               Default Value |
|------------------------------------------------|:--------------------------------------------------------------------------------:|----------------------------:|
| gcloud.loadBalancer.enabled                    |                    Enable Google Kubernetes Engine Controller                    |                       false |
| gcloud.loadBalancer.staticAddressName          | Static Address Name  For using same ip for ingress LB(need to be created before) | thingsboard-http-lb-address |
| gcloud.loadBalancer.cert.enabled               |                          Enable certificate for ingress                          |             secret password |
| gcloud.loadBalancer.cert.hosts                 |                       List hosts that will use in ingress                        |          ["www.exaple.com"] |
