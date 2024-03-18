#### Internal Zookeeper(Bitnami)

Option if you want to use internal Zookeeper that will be up and run by this chart. This section will bring
bitnami/zookeeper (https://artifacthub.io/packages/helm/bitnami/zookeeper) into this chart. If you want to add some extra
configuration, you just can put it with key internalZookeeper, and they will be passed to bitnami/zookeeper chart

| Name                           |                                                                                                    Description                                                                                                     |       Value |
|--------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|------------:|
| internalZookeeper.enable       | If enabled this option bitnami/zookeeper will be deployed. Please note that externalZookeeper.enabled: true will override this option and chart will expect that you already have configured and running zookeeper |        true |
| internalZookeeper.nameOverride |                                                                                              Internal Zookeeper name                                                                                               | "zookeeper" |

For `internalZookeeper` prefix, from table above parameters are example of simplest configuration. You can add any parameters
with this prefix from [Bitnami Zookeeper Doc`s](https://artifacthub.io/packages/helm/bitnami/zookeeper).
