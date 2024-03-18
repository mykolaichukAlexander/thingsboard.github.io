#### Internal Postgresql  (Bitnami)

Option if you want to use internal Postgresql that will be up and run by this chart. This section will bring
[bitnami/postgresql](https://artifacthub.io/packages/helm/bitnami/postgresql) into this chart. If you want to add some extra
configuration, you just can put it with key internalPostgresql, and they will be passed to bitnami/postgresql chart

| Name                             |                                                                                                          Description                                                                                                          |        Value |
|----------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|-------------:|
| internalPostgresql.enabled       | If enabled this option bitnami/postgresql will be deployed. Please note that `internalPostgresql.enabled`: true option means that you will not use externalPostgresql and want to deploy bitnami/postgresql within this chart |         true |
| internalPostgresql.nameOverride  |                                                                                         Default name override for bitnami/postgresql                                                                                          | "postgresql" |
| internalPostgresql.architecture  |                                                                        Architecture for bitnami/postgresql. Allowed values: standalone or replication                                                                         |   standalone |
| internalPostgresql.auth.username |                                                                                                    Postgresql server user                                                                                                     |     username |
| internalPostgresql.auth.password |                                                                                                Postgresql server user password                                                                                                |   standalone |
| internalPostgresql.auth.database |                                                                                              Postgresql database for Thingsboard                                                                                              |   standalone |
