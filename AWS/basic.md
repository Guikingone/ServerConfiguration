# Basic configuration

This configuration is build for simple application who need to be fast while managing small amount of data.

## EC2

First, create a simple 3 node instance :

```bash
aws ec2 run-instances --image-id _imageIdentifier_ --count _count_ --instance-type t2.micro --iam-instance-profile Name=ecsInstanceRole --key-name _sshKeysName_ --security-group-ids _securityGroup_
```

If we need to list the instances launched linked to a cluster :

```bash
aws ecs list-container-instances --cluster _clusterName_
```

## RDS PostgreSQL

First, create a simple RDS PostgreSQL instance :

```bash
aws rds create-db-instance --engine postgres --no-multi-az --no-publicly-accessible --vpc-security-group-ids _securityGroup_ --db-instance-class db.t2.micro --allocated-storage 20 --db-instance-identifier _instanceName_ --db-name _dbName_ --master-username _username_ --master-user-password _userpassword_
```

In case we need to update the DB password :

```bash
aws rds modify-db-instance --db-instance-identifier _instanceName_ --master-user-password _userpassword_
```

In order to list all the db instances :

```bash
aws rds describe-db-instances
```

If needed, we can delete the instance :

```bash
aws rds delete-db-instance --db-instance-identifier _instanceName_ --skip-final-snapshot
```

## ElastiCache

First, create a simple Redis cache instance :

```bash
aws elasticache create-cache-cluster --engine redis --security-group-ids _securityGroup_ --cache-node-type cache.t2.micro --num-cache-nodes 1 --cache-cluster-id _cacheName_
```
**_Note that the security group is mandatory for accessing the instance within other container_**

If needed, the instance can be described via :

```bash
aws elasticache describe-cache-clusters
```

Or

```bash
aws elasticache describe-cache-clusters --show-cache-node-info
```

For deleting this instance :

```bash
aws elasticache delete-cache-cluster --cache-cluster-id _cacheName_
```
