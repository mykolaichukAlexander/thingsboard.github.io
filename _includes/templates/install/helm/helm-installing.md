To install  cluster we need :

- Add repository:
  ```shell
  helm repo add thingsboard-cluster-betta https://mykolaichukalexander.github.io/thingsboard-cluster-chart/
  ```

- Install chart:
  ```shell
  helm install my-thingsboard-cluster thingsboard-cluster-betta/thingsboard-cluster --version 0.1.0
  ```

This command will install CE Thingsboard cluster in MSA mode with Kafka, Redis, and Zookeeper. As database only Postgresql.

For installing chart with already prepared config file, just add -f options with path to file. We prepared couple
files for different configuration in [Examples](#examples) section on this page.

To configure all needed cluster behavior please see [Thingsboard services parameters](#thingsboard-services-parameters)
and [Third-party services parameters](#third-party-services-parameters)


By default config, chart will install Thingsboard cluster in MSA mode with:
- web-ui - web UI for Thingsboard;
- postgresql - database;
- kafka-controller - queue;
- redis-master - cache ;
- zookeeper - coordinator for services;
- rule-engine - Thingsboard RE service;
- core - Thingsboard Core Services.
