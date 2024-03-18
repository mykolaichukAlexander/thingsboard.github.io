#### AWS ingress configuration

For EKS Ingress integration this chart has [aws-load-balancer-controller](https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html)
chart as a dependency and can be switched on and configured due prefix awscontroller.
Please, prepare a service account before and put it as variable to sub chart. This service account should have all permissions to create needed resources.
If you plan to use HTTPS for ingress controller you need to create/import certificate into [Certificate Manager](https://aws.amazon.com/certificate-manager/) and just add this option via `awscontroller.cert.enabled`
and put `awscontroller.cert.arn` and list of hosts `awscontroller.cert.hosts`

Values for sub chart that will add LB controllers into cluster:

| Name                                |                                                     Description                                                      |       Default Value |
|-------------------------------------|:--------------------------------------------------------------------------------------------------------------------:|--------------------:|
| awscontroller.enabled               |                                            Enable EKS ingress controller                                             |               false |
| awscontroller.clusterName           |                                          Eks cluster name that was created                                           |                     |
| awscontroller.serviceAccount.create |   If added withAddonPolicies then can be true, cause cluster will have permission to create right service account    |               false |
| awscontroller.serviceAccount.name   | Name of created (or what will be created) service account that will be Created automatically from role that provided |                  "" |
| awscontroller.cert.enabled          |                                                     Enable HTTPS                                                     |               false |
| awscontroller.cert.arn              |                               ARN of created certificate from  **Certificate Manager**                               |                     |
| awscontroller.cert.hosts            |                                                    List of hosts                                                     | ["www.example.com"] |


Example:
````yaml
awscontroller:
  enabled: false
  clusterName: "thingsboard-helm"
  serviceAccount:
    create: false
    name: tb-cluster-load-balancer-controller # created before
````

You need to fill ***clusterName*** with valid name of eks cluster that was created before and
***serviceAccount.name*** with prepared service account. To see how to creat it see [examples](#examples)
