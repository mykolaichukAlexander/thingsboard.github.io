### Installation Parameters


| Name                    |                                                                                                                                                                                                                 Description                                                                                                                                                                                                                 |                         Value |
|-------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|------------------------------:|
| installation.msa        |                                                                                    Thingsboard architecture Type. Thingsboard can run in different configurations to meet different needs. To decide in what configuration you should run your cluster please [see](https://thingsboard.io/docs/pe/reference/#monolithic-vs-microservices-architecture).                                                                                    |                         false |
| installation.installTb  | This field is responsible for the installation process of Thingsboard. The installation process will create all needed database tables (in PostgreSQL in case of only "Postgres Mode" for Timeseries. Or in PostgreSQL in Cassandra) in the case of "hybrid mode". For more information on how to choose the most suitable option for you please [see](https://thingsboard.io/docs/pe/reference/#sql-vs-nosql-vs-hybrid-database-approach). |                         false |
| installation.loadDemo   |                                                                                                                                                                Works only with installation.installTb: true. This option will load into database some prepared data for you.                                                                                                                                                                |                         false |
| installation.pe         |                                                                                                                                                 Switch on Professional Edition mode. For more information please [see](https://thingsboard.io/docs/getting-started-guides/helloworld-pe/).                                                                                                                                                  |                         false |
| installation.licenseKey |                                                                                                                If you plan to use the Professional Edition version of Thingsboard you need to provide this key. You can get this key from Thingsboard team. In the case of Community Edition, you can skip this field empty.                                                                                                                |                            "" |
| dockerAuth.registry     |                                                                                                                                                                                                   Docker registry for Thingsboard images                                                                                                                                                                                                    | "https://index.docker.io/v1/" |
| dockerAuth.username     |                                                                                                                                                                                            Docker username on which pull secret will be created                                                                                                                                                                                             |                            "" |
| dockerAuth.password     |                                                                                                                                                                                          Docker user password on which pull secret will be created                                                                                                                                                                                          |                            "" |



### Global Parameters

| Name                   |            Description             |   Value |
|------------------------|:----------------------------------:|--------:|
| global.imagePullSecret | Global Docker registry secret name | regcred |


### Thingsboard Node Parameters

> Node means that in case of monolith this parameters will configure node pod that contains Core/Rule engine functionality,
> in case of msa - just core.


| Name                                   |                                                                                                                                  Description                                                                                                                                   |                     Value |
|----------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|--------------------------:|
| node.image.repository                  |                                                                                              Repository option that has the highest priority and will override global.repository                                                                                               |       thingsboard/tb-node |
| node.image.tag                         |                                                                                                     Tag option that has the highest priority and will override global.tag                                                                                                      | Chart Application Version |
| node.imagePullPolicy                   |                                                                                                                        Node/core pull policy for image                                                                                                                         |                    Always |
| node.statefulSet.replicas              |                                                                                                                     Replica count for node(core) services                                                                                                                      |                         1 |
| node.ports                             |                                                                 List of ports for node(core) service, you can just add your custom ports as list entries and their will be rendered and added to node manifest                                                                 |                           |
| node.nodeSelector                      | Node selector for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. Usually it is Map type. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details |                        {} |
| node.affinity                          |               Affinity for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details                |                        {} |
| node.customEnv                         |                                                  A Map for custom environment variable for node(core) service. If not empty, all env vars will be added on config map and will path to pods. Useful while custom developing.                                                   |                        {} |
| node.readinessProbe.httpGet.path       |                                                                                                                       Node/core path for readiness probe                                                                                                                       |                    /login |
| node.readinessProbe.httpGet.port       |                                                                                                                       Node/core port for readiness probe                                                                                                                       |                      8080 |
| node.livenessProbe.httpGet.path        |                                                                                                                       Node/core path for liveness probe                                                                                                                        |                    /login |
| node.livenessProbe.httpGet.port        |                                                                                                                       Node/core port for liveness probe                                                                                                                        |                      8080 |
| node.livenessProbe.initialDelaySeconds |                                                                                                                        Node/core initial delay seconds                                                                                                                         |                       460 |
| node.livenessProbe.timeoutSeconds      |                                                                                                                           Node/core timeout seconds                                                                                                                            |                        10 |
| node.restartPolicy                     |                                                                                                                          Node/core pod restart policy                                                                                                                          |                    Always |
| node.securityContext.runAsUser         |                                                                                                                             Node/core run as user                                                                                                                              |                       799 |
| node.securityContext.runAsNonRoot      |                                                                                                                           Node/core run as non root                                                                                                                            |                      true |
| node.securityContext.fsGroup           |                                                                                                                               Node/core fs group                                                                                                                               |                       799 |
| node.persistence.enabled               |                          Persistence layer for node pods. In case of Professional Edition it is required for managing license. Or if you plan to use custom extensions with saving some state that need to "survive" pod lifetime events ot updates.                           |                      true |
| node.persistence.existingClaim         |                                                                                                                            Node/core existing claim                                                                                                                            |                        "" |
| node.persistence.size                  |                                                                                                                   Node/core pvc size that will be requested                                                                                                                    |                       1Gi |
| node.persistence.accessModes           |                                                                                                                             Node/core access modes                                                                                                                             |       [ "ReadWriteOnce" ] |
| node.persistence.storageClass          |                                                                                                                          Node/core storage class name                                                                                                                          |                           |
| node.resources.limits.cpu              |                                                                                                                                   Limit cpu                                                                                                                                    |                   "2000m" |
| node.resources.limits.memory           |                                                                                                                                  Limit memory                                                                                                                                  |                    3000Mi |
| node.resources.requests.cpu            |                                                                                                                                  Requests cpu                                                                                                                                  |                   "1000m" |
| node.resources.requests.memory         |                                                                                                                                Requests memory                                                                                                                                 |                    2000Mi |

Default ports `node.ports` are:
```yaml
  ports:
   - name: http
     value: 8080
   - name: edge
     value: 7070
   - name: grpc
     value: 9090
   ```

***node.nodeSelector*** - Node selector for choosing nodes for scheduling pods.
[See](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) for more details
Example:
```yaml
  nodeSelector:
    disktype: ssd
```

***node.affinity*** - Affinity for choosing nodes for scheduling pods.
[See](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) for more details
Example:
```yaml
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: topology.kubernetes.io/zone
                operator: In
                values:
                  - antarctica-east1
                  - antarctica-west1
```

***node.customEnv*** - A Map for custom environment variable for node(core) service. If not empty, all env vars will be added on config map
and will path to pods. Useful while custom developing.
Example:
```yaml
  customEnv:
    TEST: test
```

### Thingsboard Rule Engine Parameters


| Name                                     |                                                                                                                                 Description                                                                                                                                  |                     Value |
|------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|--------------------------:|
| engine.image.repository                  |                                                                                            RE Repository option that has the highest priority and will override global.repository                                                                                            |       thingsboard/tb-node |
| engine.image.tag                         |                                                                                                   RE Tag option that has the highest priority and will override global.tag                                                                                                   | Chart Application Version |
| engine.imagePullPolicy                   |                                                                                                                           RE pull policy for image                                                                                                                           |                    Always |
| engine.statefulSet.replicas              |                                                                                                                    Replica count for rule engine services                                                                                                                    |                         1 |
| engine.ports                             |                                                            List of ports for rule engine service, you can just add your custom ports as list entries and their will be rendered and added to rule engine manifest                                                            |                           |
| engine.nodeSelector                      | RE selector for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. Usually it is Map type. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details |                        {} |
| engine.affinity                          |             RE Affinity for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details             |                        {} |
| engine.customEnv                         |                                                 A Map for custom environment variable for node(core) service. If not empty, all env vars will be added on config map and will path to pods. Useful while custom developing.                                                  |                        {} |
| engine.readinessProbe.httpGet.path       |                                                                                                                         RE path for readiness probe                                                                                                                          |                    /login |
| engine.readinessProbe.httpGet.port       |                                                                                                                         RE port for readiness probe                                                                                                                          |                      8080 |
| engine.livenessProbe.httpGet.path        |                                                                                                                          RE path for liveness probe                                                                                                                          |                    /login |
| engine.livenessProbe.httpGet.port        |                                                                                                                          RE port for liveness probe                                                                                                                          |                      8080 |
| engine.livenessProbe.initialDelaySeconds |                                                                                                                           RE initial delay seconds                                                                                                                           |                       460 |
| engine.livenessProbe.timeoutSeconds      |                                                                                                                              RE timeout seconds                                                                                                                              |                        10 |
| engine.restartPolicy                     |                                                                                                                            RE pod restart policy                                                                                                                             |                    Always |
| engine.securityContext.runAsUser         |                                                                                                                               RE  run as user                                                                                                                                |                       799 |
| engine.securityContext.runAsNonRoot      |                                                                                                                              RE run as non root                                                                                                                              |                      true |
| engine.securityContext.fsGroup           |                                                                                                                                 RE fs group                                                                                                                                  |                       799 |
| engine.persistence.enabled               |                         Persistence layer for node pods. In case of Professional Edition it is required for managing license. Or if you plan to use custom extensions with saving some state that need to "survive" pod lifetime events ot updates.                          |                      true |
| engine.persistence.existingClaim         |                                                                                                                              RE existing claim                                                                                                                               |                        "" |
| engine.persistence.size                  |                                                                                                                                 RE affinity                                                                                                                                  |                       1Gi |
| engine.persistence.accessModes           |                                                                                                                               RE access modes                                                                                                                                |       [ "ReadWriteOnce" ] |
| engine.persistence.storageClass          |                                                                                                                            RE storage class name                                                                                                                             |                           |
| engine.resources.limits.cpu              |                                                                                                                                  Limit cpu                                                                                                                                   |                   "2000m" |
| engine.resources.limits.memory           |                                                                                                                                 Limit memory                                                                                                                                 |                    3000Mi |
| engine.resources.requests.cpu            |                                                                                                                                 Requests cpu                                                                                                                                 |                   "1000m" |
| engine.resources.requests.memory         |                                                                                                                               Requests memory                                                                                                                                |                    2000Mi |


### Thingsboard Web Report Parameters

Thingsboard Web Report Service configuration section

| Name                             |                                                                                                                                 Description                                                                                                                                  |                     Value |
|----------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|--------------------------:|
| report.enabled                   |                                                                                                               Enable of disable web report service in cluster.                                                                                                               |                      true |
| report.image.repository          |                                                                                       Repository that will be used for web report service. If blank - default repository will be used.                                                                                       |                           |
| report.image.tag                 |                                                                                              Tag that will be used for web report service. If blank - default tag will be used.                                                                                              | Chart Application Version |
| report.deployment.replicas       |                                                                                                                     WR Default replica count for service                                                                                                                     |                         1 |
| report.nodeSelector              | WR selector for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. Usually it is Map type. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details |                        {} |
| report.affinity                  |             WR Affinity for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details             |                        {} |
| report.resources.limits.cpu      |                                                                                                                                  Limit cpu                                                                                                                                   |                   "2000m" |
| report.resources.limits.memory   |                                                                                                                                 Limit memory                                                                                                                                 |                    3000Mi |
| report.resources.requests.cpu    |                                                                                                                                 Requests cpu                                                                                                                                 |                   "1000m" |
| report.resources.requests.memory |                                                                                                                               Requests memory                                                                                                                                |                    2000Mi |



### Thingsboard Web UI Parameters (for msa installation type)

Thingsboard Web UI Service configuration section

| Name                          |                                                                                                                                   Description                                                                                                                                    |                     Value |
|-------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|--------------------------:|
| web.enabled                   |                                                                                                                 Enable of disable web report service in cluster.                                                                                                                 |                      true |
| web.image.repository          |                                                                                           Repository that will be used for web ui service. If blank - default repository will be used                                                                                            |                           |
| web.image.tag                 |                                                                                                  Tag that will be used for web ui service. If blank - default tag will be used                                                                                                   | Chart Application Version |
| web.deployment.replicas       |                                                                                                                      Web UI replicas that will be deployed                                                                                                                       |                         1 |
| web.nodeSelector              | Web UI selector for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. Usually it is Map type. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details |                        {} |
| web.affinity                  |             Web UI Affinity for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details             |                        {} |
| web.resources.limits.cpu      |                                                                                                                                 Web UI limit cpu                                                                                                                                 |                    "100m" |
| web.resources.limits.memory   |                                                                                                                               Web UI limit memory                                                                                                                                |                     100Mi |
| web.resources.requests.cpu    |                                                                                                                               Web UI requests cpu                                                                                                                                |                    "100m" |
| web.resources.requests.memory |                                                                                                                              Web UI requests memory                                                                                                                              |                     100Mi |


### Thingsboard JS Executor Parameters
Thingsboard JavaScript Executor Service configuration section
JavaScripts executor executes all js scripts on Rule Engine and Integrations etc.
Now Thingsboard has alternative such as TBEL (https://thingsboard.io/docs/user-guide/tbel/).
But if you plan use JavaScript js.enabled should be true

| Name                         |                                                                                                                                      Description                                                                                                                                      |  Value |
|------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|-------:|
| js.enabled                   |                                                                                                                   Enable of disable js-executor service in cluster.                                                                                                                   |  false |
| js.image.repository          |                                                                                           Repository that will be used for js-executor service. If blank - default repository will be used                                                                                            |        |
| js.image.tag                 |                                                                                                  Tag that will be used for js-executor service. If blank - default tag will be used                                                                                                   |        |
| js.deployment.replicas       |                                                                                                                      Js Executor replicas that will be deployed                                                                                                                       |      5 |
| js.nodeSelector              | Js Executor selector for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. Usually it is Map type. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details |     {} |
| js.affinity                  |             Js Executor Affinity for choosing nodes for scheduling pods. Note that this is default kubernetes object, so you need to specify whole object, not just labels. See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ for more details             |     {} |
| js.resources.limits.cpu      |                                                                                                                                 Js Executor limit cpu                                                                                                                                 | "100m" |
| js.resources.limits.memory   |                                                                                                                               Js Executor limit memory                                                                                                                                |  100Mi |
| js.resources.requests.cpu    |                                                                                                                               Js Executor requests cpu                                                                                                                                | "100m" |
| js.resources.requests.memory |                                                                                                                              Js Executor requests memory                                                                                                                              |  100Mi |


### Thingsboard Transports Parameters

Transport configuration. [Full details](https://thingsboard.io/docs/reference/msa/)
Thingsboard has various options for different protocols that can help you connect devices with
Thingsboard platform. In this configuration *transports* it is a Map like structure. 
Example:
```yaml
transports:
  http: {transport config object}
  mqtt: {transport config object}
```

Keys for transports can be `http`, `coap`, `lwm2m`, `snmp`, `mqtt`

As `transport config object` you can customise next parameters:

| Name                                    |                                                                                 Description                                                                                 |                                         Value |
|-----------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|----------------------------------------------:|
| TRANSPORT_KEY.enabled                   |                                                             Enable or disable this transport into your cluster                                                              |                                         false |
| TRANSPORT_KEY.name                      |                                      Name that will be used for kubernetes resources like sts and services for TRANSPORT_KEY transport                                      | http-transport `(example for http transport)` |
| TRANSPORT_KEY.image.repository          |                                                  Transport custom repository. When blank - default repository will be used                                                  |                                               |
| TRANSPORT_KEY.image.tag                 |                                                     Transport custom tag. When blank - default repository will be used                                                      |                     Chart Application Version |
| TRANSPORT_KEY.replicas                  |                                                                             Transport replicas                                                                              |                                             1 |
| TRANSPORT_KEY.ports                     | Transport ports that container will use. Be sure that this port will match with HTTP_BIND_PORT in env variables. Ports yaml value is similar to Node/Core/Rule engine ports |                                               |
| TRANSPORT_KEY.env                       |                                 Environment variables for http transport service. Charts already has a list of preconfigured env variables                                  |                                               |
| TRANSPORT_KEY.nodeSelector              |                                                                           Transport node selector                                                                           |                                            {} |
| TRANSPORT_KEY.affinity                  |                                                                             Transport affinity                                                                              |                                            {} |
| TRANSPORT_KEY.resources.limits.cpu      |                                                                             Transport limit cpu                                                                             |                                       "1000m" |
| TRANSPORT_KEY.resources.limits.memory   |                                                                           Transport limit memory                                                                            |                                        2000Mi |
| TRANSPORT_KEY.resources.requests.cpu    |                                                                           Transport requests cpu                                                                            |                                        "500m" |
| TRANSPORT_KEY.resources.requests.memory |                                                                          Transport requests memory                                                                          |                                         500Mi |
