#### Internal Redis cluster(Bitnami)

Option if you want to use internal redis cluster that will be up and run by this chart. This section will bring
[bitnami/redis-cluster](https://artifacthub.io/packages/helm/bitnami/redis-cluster) into this chart. If you want to add some extra
configuration, you just can put it with key internalRedisCluster, and they will be passed to bitnami/redis-cluster chart
internalRedisCluster:


| Name                              |                        Description                        |          Value |
|-----------------------------------|:---------------------------------------------------------:|---------------:|
| internalRedisCluster.enabled      | Enable or disable bitnami/redis-cluster into your cluster |          false |
| internalRedisCluster.nameOverride |      Default name override for bitnami/redis-cluster      |        "redis" |
| internalRedisCluster.usePassword  |       Enable or disable bitnami/redis-cluster auth        |           true |
| internalRedisCluster.password     |                  Default redis password                   | "testPassword" |
