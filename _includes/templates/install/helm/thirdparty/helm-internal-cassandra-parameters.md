#### Internal Cassandra (Bitnami)

Option if you want to use internal Cassandra that will be up and run by this chart. This section will bring
[bitnami/cassandra](https://artifacthub.io/packages/helm/bitnami/cassandra) into this chart. If you want to add some extra
configuration, you just can put it with key internalCassandra, and they will be passed to bitnami/cassandra chart
If *externalCassandra.enabled* = false and *internalCassandra.enabled* = false that Thingsboard will be configured to work
only with Postgresql


| Name                                  |                                                                                                    Description                                                                                                     |          Value |
|---------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|---------------:|
| internalCassandra.enabled             | If enabled this option bitnami/zookeeper will be deployed. Please note that externalCassandra.enabled: true will override this option and chart will expect that you already have configured and running cassandra |          false |
| internalCassandra.replicationStrategy |                                                                           Default Replication Strategy for Keyspace that will be created                                                                           | SimpleStrategy |
| internalCassandra.replicaCount        |                                                                                             Default Replication count                                                                                              |              1 |
| internalCassandra.cluster.datacenter  |                                                                                             Cassandra datacenter name                                                                                              |  "datacenter1" |
| internalCassandra.nameOverride        |                                                                                              Internal Cassandra name                                                                                               |    "cassandra" |
| internalCassandra.initDBConfigMap     |                                                                                         Internal Cassandra init config map                                                                                         | cassandra-init |
| internalCassandra.dbUser.user         |                                                                                              Internal Cassandra user                                                                                               |      cassandra |
| internalCassandra.dbUser.password     |                                                                                            Internal Cassandra password                                                                                             |      cassandra |

For `internalCassandra` prefix, from table above parameters are example of simplest configuration. You can add any parameters
with this prefix from [Bitnami Cassandra Doc`s](https://artifacthub.io/packages/helm/bitnami/cassandra).


If you customise and use internal cassandra we recommend to create a new node group or node pools for your cassandra deployments, you can find information how to do this
by following links:
- [AKS](https://thingsboard.io/docs/user-guide/install/pe/cluster/azure-microservices-setup/#52-cassandra);
- [EKS](https://thingsboard.io/docs/user-guide/install/pe/cluster/aws-microservices-setup/#step-42-cassandra);
- [GKE](https://thingsboard.io/docs/user-guide/install/pe/cluster/gcp-microservices-setup/#step-52-cassandra-optional).

And use `nodeSelector` of affinities for using new created pools.

`cassandra-init` configmap it is pretty simple config that will be used for creating cassandra keyspace and has the following structure
```yaml
...
data:
  "01-init.cql": |
    CREATE KEYSPACE IF NOT EXISTS thingsboard
      WITH REPLICATION = {
        'class': 'SimpleStrategy',
        'replication_factor' : 1
      };
```

Before using cassandra **not on dev** please create init script that suitable for your infrastructure. You can 
set it using: ***internalCassandra.initDBConfigMap.cassandra-init***

