#### External Zookeeper

When you already deploy Zookeeper by yourself or using some sort of service this section should be filled.
By external means that zookeeper will be managed by not this chart.
If msa mode on, externalZookeeper.enabled = true or internalZookeeper.enabled = true  is required

| Name                           |                                                                                          Description                                                                                           |       Value |
|--------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|------------:|
| externalZookeeper.enable       | If this option is true, chart will know that it should expect external kafka. external options are the highest in priority and other zookeeper options like internalZookeeper will be ignored. |       false |
| externalZookeeper.host         |                                                                                    External zookeeper host                                                                                     |             |
| externalZookeeper.port         |                                                                                    External zookeeper port                                                                                     |             |


