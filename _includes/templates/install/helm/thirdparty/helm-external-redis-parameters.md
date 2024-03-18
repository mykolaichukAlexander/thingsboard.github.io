#### External Redis

When you already deploy redis by yourself or using some sort of service this section should be filled.
By external means that redis will be managed  by not this chart.

If this option is true, chart will know that it should expect external redis. external options are the highest
in priority and other redis options like internalRedis and internalRedisCluster will be ignored.


| Name                   |                                                                                                   Description                                                                                                   | Value |
|------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|------:|
| externalRedis.enable   | If this option is true, chart will know that it should expect external redis. external options are the highest in priority and other redis options like internalRedis and internalRedisCluster will be ignored. | false |
| externalRedis.hosts    |                                                                                 Hosts list for external redis. Format hust:port                                                                                 |    "" |
| externalRedis.cluster  |                                                                        Let to know to Thingsboard that redis is running in cluster mode                                                                         | false |
| externalRedis.password |                                                                                     Password for external redis if expected                                                                                     |    "" |


