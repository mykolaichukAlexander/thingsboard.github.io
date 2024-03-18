#### External Cassandra

When you already deploy Cassandra by yourself or using some sort of service this section should be filled.
By external means that cassandra will be managed by not this chart
Thingsboard keyspace should be created before install.
If `externalCassandra.enabled` = false and `internalCassandra.enabled` = false that Thingsboard will be configured to work
only with Postgresql

| Name                                  |                                                                                            Description                                                                                             |            Value |
|---------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|-----------------:|
| externalCassandra.enabled             | If this option is true, chart will know that it should expect external cassandra. external options are the highest in priority and other cassandra options like internalCassandra will be ignored. |            false |
| externalCassandra.hosts               |                                                                                      External cassandra host                                                                                       |      "cassandra" |
| externalCassandra.hosts               |                                                                                      External cassandra port                                                                                       |           "9042" |
| externalCassandra.user                |                                                                                      External Cassandra user                                                                                       |      "cassandra" |
| externalCassandra.password            |                                                                                  External Cassandra user password                                                                                  |      "cassandra" |
| externalCassandra.datacenter          |                                                                                   External Cassandra datacenter                                                                                    |            "dc1" |

