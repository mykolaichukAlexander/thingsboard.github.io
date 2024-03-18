#### Thingsboard monolith cluster

For installing monolith thingsboard(postgresql only) in Kubernetes cluster you can start from next values file:
```yaml
installation:
  msa: false
  pe: false
internalKafka:
  enabled: false
internalRedis:
  enabled: false
internalZookeeper:
  enabled: false
internalPostgresql:
  enabled: true
  auth:
    username: "root"
    password: "root"
    database: "thingsboard"

defaultIngress:
  enabled: true
```

For running Thingsboard with Cassandra just add to this config:
```yaml
internalCassandra:
  enabled: true
```
