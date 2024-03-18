This chart bootstraps a [Thingsboard](https://thingsboard.io/) deployment on a [Kubernetes](https://kubernetes.io/) cluster using the [Helm](https://helm.sh/) package manager.

ThingsBoard is an open-source IoT platform that enables rapid development, management, and scaling of IoT projects.

Thingsboard cluster can be deployed in different configurations to suit various needs.
- [Monolith](https://thingsboard.io/docs/reference/monolithic/) Thingsboard instance that will run with Postgresql database should be a good start of adventure.
- [Microservice](https://thingsboard.io/docs/reference/msa/) architecture (next MSA) Thingsboard cluster it is a good choice for cluster option when we need the scalability of
  separate parts that helps you to reach height availability and easily processes and analyze a big amount of data.
  MSA mode requires third-party services like Kafka for `queue`, Zookeeper as `service coordinator`, and Redis for `cache`.

As Databases Thingsboard can use PostgresSQL or PostgresSQL and Cassandra. Cassandra is usually a wise choice if you plan to use
a large amount of data. For more details about architecture please visit [CE docs](https://thingsboard.io/docs/reference/) for CE and [PE docs](https://thingsboard.io/docs/pe/reference/) for PE.


> **_NOTE:_**  Thingsboard by itself supports various services for queue, and cache, but this chart for now supports only services noticed above.


For more faster and easier start this chart is "out of the box" depends on thirds party charts like:
- [Redis](https://artifacthub.io/packages/helm/bitnami/redis);
- [Redis-cluster](https://artifacthub.io/packages/helm/bitnami/redis-cluster);
- [Cassandra](https://artifacthub.io/packages/helm/bitnami/cassandra);
- [Postgresql](https://artifacthub.io/packages/helm/bitnami/postgresql);
- [Kafka](https://artifacthub.io/packages/helm/bitnami/kafka);
- [Zookeeper](https://artifacthub.io/packages/helm/bitnami/zookeeper).

All these sub-charts are [Official bitnami charts](https://bitnami.com/). To override some values from this sub-charts please user prefix:

| Service name | sub chart service prefix | Your outer implementation prefix |
|-------------:|:------------------------:|:--------------------------------:|
|        Redis |      internalRedis       |          externalRedis           |
|        Kafka |      internalKafka       |          externalKafka           |
|    Cassandra |    internalCassandra     |        externalCassandra         |
|    Zookeeper |    internalZookeeper     |        externalZookeeper         |
|   Postgresql |    internalPostgresql    |        externalPostgresql        |


All **external** prefixes have a higher priority and will overwrite default **internals**.



> :warning: **Warning:**  Please don`t use base configured third-party services in production before configuring them.
> For configuration you can use [Official bitnami docs](https://bitnami.com/)
