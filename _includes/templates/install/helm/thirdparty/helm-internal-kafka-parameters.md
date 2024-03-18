#### Internal kafka (Bitnami)
Option if you want to use internal Kafka that will be up and run by this chart. This section will bring
bitnami/kafka (https://artifacthub.io/packages/helm/bitnami/kafka) into this chart. If you want to add some extra
configuration, you just can put it with key internalKafka, and they will be passed to bitnami/kafka chart



Option if you want to use internal Kafka that will be up and run by this chart. This section will bring
bitnami/kafka (https://artifacthub.io/packages/helm/bitnami/kafka) into this chart. If you want to add some extra
configuration, you just can put it with key internalKafka, and they will be passed to bitnami/kafka chart

| Name                       |                                                                                              Description                                                                                               |   Value |
|----------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|--------:|
| internalKafka.enable       | If enabled this option bitnami/kafka will be deployed. Please note that externalKafka.enabled: true will override this option and chart will expect that you already have configured and running kafka |    true |
| internalKafka.nameOverride |                                                                                Default name override for bitnami/kafka                                                                                 | "kafka" |
| internalKafka.replicaCount |                                                                                Default replica count for bitnami/kafka                                                                                 |       1 |

For `internalKafka` prefix, from table above parameters are example of simplest configuration. You can add any parameters
with this prefix from [Bitnami Kafka Doc`s](https://artifacthub.io/packages/helm/bitnami/kafka).
