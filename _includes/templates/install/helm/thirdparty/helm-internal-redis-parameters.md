#### Internal Redis (Bitnami)

Option if you want to use internal redis that will be up and run by this chart. This section will bring
[bitnami/redis](https://artifacthub.io/packages/helm/bitnami/redis) into this chart. If you want to add some extra
configuration, you just can put it with key internalRedis, and they will be passed to bitnami/redis chart

| Name                              |                                         Description                                         |          Value |
|-----------------------------------|:-------------------------------------------------------------------------------------------:|---------------:|
| internalRedis.enabled             |                      Enable or disable bitnami/redis into your cluster                      |           true |
| internalRedis.nameOverride        |                           Default name override for bitnami/redis                           |        "redis" |
| internalRedis.architecture        |        Architecture for bitnami/redis. Allowed values: `standalone` or `replication`        |     standalone |
| internalRedis.auth.enabled        |                                         Redis auth                                          |           true |
| internalRedis.auth.password       |                                       Redis password                                        | "testPassword" |



