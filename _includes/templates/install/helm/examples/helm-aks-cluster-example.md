#### 1. EKS Init

##### Create Cluster
*If you already have a cluster you can skip this step.*

Before installing chart we need create a cluster.

To create cluster on AWS you can follow [Official AWS documentation](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)
or our prepared configuration for creating cluster.

First you need to install and configurate eksctl. To do so please follow [next instruction](https://eksctl.io/installation/)

For easier cluster creation, ThingsBoard team already prepared cluster.yml file that you can use with eksctl:
```yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

# Specify desired availability zones. Don't forget to update the 'metadata.region' parameter to match availability zones.
availabilityZones: [us-east-1a,us-east-1b,us-east-1c]

metadata:
  name: super-msa-helm-testing
  # Specify the desired aws region. Don't forget to update the 'availabilityZones' parameter to match the region.
  region: us-east-1
  version: "1.27"

iam:
  withOIDC: true

addons:
  - name: aws-ebs-csi-driver

managedNodeGroups:
  - name: tb-node
    instanceType: m5.xlarge
    desiredCapacity: 3
    maxSize: 3
    minSize: 3
    labels: { role: tb-node }
    # EC2 nodes will be launched in the private subnet and will not be accessible via SSH from the internet.
    privateNetworking: true
    # this option gain additional policies that allow you create load balancers for ingress and transports
    iam:
      withAddonPolicies:
        awsLoadBalancerController: true
  # Uncomment this section if you plan to install and use Cassandra
#  - name: cassandra-1a
#    instanceType: m5.xlarge
#    desiredCapacity: 1
#    maxSize: 1
#    minSize: 1
#    labels: { role: cassandra }
#    availabilityZones: ["us-east-1a"]
#    privateNetworking: true
#    iam:
#      withAddonPolicies:
#        awsLoadBalancerController: true
#  - name: cassandra-1b
#    instanceType: m5.xlarge
#    desiredCapacity: 1
#    maxSize: 1
#    minSize: 1
#    labels: { role: cassandra }
#    availabilityZones: ["us-east-1b"]
#    privateNetworking: true
#    iam:
#      withAddonPolicies:
#        awsLoadBalancerController: true
#  - name: cassandra-1c
#    instanceType: m5.xlarge
#    desiredCapacity: 1
#    maxSize: 1
#    minSize: 1
#    labels: { role: cassandra }
#    iam:
#      withAddonPolicies:
#        awsLoadBalancerController: true
#    availabilityZones: ["us-east-1c"]
```

Where:
- **region** - should be the AWS region where you want your cluster to be located (the default value is us-east-1)
- **availabilityZones** - should specify the exact IDs of the region’s availability zones (the default value is [us-east-1a,us-east-1b,us-east-1c])
- **instanceType** - the type of the instance with TB node (the default value is m5.xlarge)

When you modify this file with all needed for you configs, you can create cluster
```shell
eksctl create cluster -f cluster.yml
```

After command will finish you kubeclt should automatically configuring to use newly created cluster.
To confirm this just run
```shell
kubectl get nodes
```


#### 2. EKS install chart

##### Helm command

To install Thingsboard cluster you need to execute following command:
```shell
helm install release-name thingsboard-cluster-betta/thingsboard-cluster -f eks-monolith-rds-postgres.yml --set installation.installTb=true
```
where:
- `release-name` - your chart release name;
- `eks-monolith-rds-postgres.yml` - custom values file;
- `--set installation.installTb=true` - if you running thingsboard first time this command will said to chart to install database tables;
- `--set installation.loadDemo=true` - if you want to load demo data.

There are a list of custom values file examples:
- Monolith Thingsboard CE with RDS database (Postgresql only):

```yaml
installation:
  msa: false
  pe: false

#This is monolith example install so Kafka, Redis and Zookeeper should be off, but because they enabled by default
# in this case we should explicitly switch them off
internalKafka:
  enabled: false
internalRedis:
  enabled: false
internalZookeeper:
  enabled: false

internalPostgresql:
  enabled: false

# This rds Instance was created before. Make sure your nodes in cluster can access
# RDS instance , you need to create new inbound rule from cluster security group to security group of Postgres RDS (https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.Scenarios.html fpr more details)
# And auth.database in this case should be created before start
externalPostgresql:
  # Postgresql server host
  host: "YOUR_RDS_HOST"
  # Postgresql server port
  port: 5432
  # Postgresql server user
  username: "postgres"
  # Postgresql server user password
  password: "qwerty123"
  # Postgresql for Thingsboard
  database: "thingsboard1"

awscontroller:
  enabled: true
  clusterName: "msa-helm-testing"
  serviceAccount:
    create: true
    name: tb-cluster-load-balancer-controller
```

- MSA Thingsboard CE with RDS database (Postgresql only):

```yaml
installation:
  msa: true
  pe: false

#This is monolith example install so Kafka, Redis and Zookeeper should be off, but because they enabled by default
# in this case we should explicitly switch them off
internalKafka:
  enabled: true
internalRedis:
  enabled: true
internalZookeeper:
  enabled: true

internalPostgresql:
  enabled: false

# This rds Instance was created before. Make sure your nodes in cluster can access
# RDS instance , you need to create new inbound rule from cluster security group to security group of Postgres RDS (https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.Scenarios.html fpr more details)
# And auth.database in this case should be created before start
externalPostgresql:
  # Postgresql server host
  host: "YOUR_RDS_HOST"
  # Postgresql server port
  port: 5432
  # Postgresql server user
  username: "postgres"
  # Postgresql server user password
  password: "qwerty123"
  # Postgresql database for Thingsboard
  database: "thingsboard"

node:
  statefulSet:
    replicas: 2

engine:
  statefulSet:
    replicas: 2

awscontroller:
  enabled: true
  clusterName: "super-msa-helm-testing"
  serviceAccount:
    create: true
    name: tb-cluster-load-balancer-controller
```


- MSA Thingsboard CE with RDS database (Postgresql and Cassandra):

```yaml
installation:
  msa: true
  pe: false

#This is monolith example install so Kafka, Redis and Zookeeper should be off, but because they enabled by default
# in this case we should explicitly switch them off
internalKafka:
  enabled: true
  replicaCount: 3
internalRedis:
  enabled: true
internalZookeeper:
  enabled: true

internalPostgresql:
  enabled: false

# This rds Instance was created before. Make sure your nodes in cluster can access
# RDS instance , you need to create new inbound rule from cluster security group to security group of Postgres RDS (https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.Scenarios.html fpr more details)
# And auth.database in this case should be created before start
externalPostgresql:
  # Postgresql server host
  host: "YOUR_RDS_HOST"
  # Postgresql server port
  port: 5432
  # Postgresql server user
  username: "YOUR_RDS_USERNAME"
  # Postgresql server user password
  password: "YOUR_RDS_PASSWORD"
  # Postgresql database for Thingsboard (should be created before)
  database: "thingsboard"


internalCassandra:
  enabled: true
  replicaCount: 3
  nodeSelector:
    role: cassandra

awscontroller:
  enabled: true
  clusterName: "super-msa-helm-testing"
  serviceAccount:
    create: true
    name: tb-cluster-load-balancer-controller
```
