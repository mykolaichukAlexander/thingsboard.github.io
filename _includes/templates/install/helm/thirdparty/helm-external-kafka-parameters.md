#### External Kafka

When you already deploy kafka by yourself or using some sort of service this section should be filled.
By external means that kafka will be managed by not this chart.

| Name                                |                                                                                      Description                                                                                       |               Value |
|-------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|--------------------:|
| externalKafka.enable                | If this option is true, chart will know that it should expect external kafka. external options are the highest in priority and other kafka options like internalKafka will be ignored. |               false |
| externalKafka.hosts                 |                                                                                  External Kafka host                                                                                   |        "kafka:9092" |

