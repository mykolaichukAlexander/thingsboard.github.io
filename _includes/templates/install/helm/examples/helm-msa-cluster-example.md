#### Thingsboard msa cluster

For installing msa thingsboard(postgresql only) in Kubernetes cluster you can start from next values file:
```yaml
installation:
  msa: true
  pe: false
transports:
  http:
    enabled: true
report:
  enabled: false
js:
  enabled: true
  deployment:
    replicaCount: 2
internalPostgresql:
  enabled: true
  auth:
    username: "root"
    password: "root"
    database: "thingsboard"

internalRedis:
  enabled: true

internalKafka:
  enabled: true

defaultIngress:
  enabled: true

```

For running Thingsboard with Cassandra just add to this config:
```yaml
internalCassandra:
  enabled: true
```
