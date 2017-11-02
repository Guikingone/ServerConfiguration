# AWS - configuration

## Security configuration (IAM)

### Security

First, create a new security group :

```bash
aws ec2 create-security-group --group-name _groupname_ --description 'Description of the Group'
```

#### Create an SSH key pair

First, use the ec2 shortcut :

```bash
aws ec2 create-key-pair --key-name _nameDesired_ --query 'KeyMaterial' --output text > ~ /.ssh/aws-keys.pem
```

Then limit the access :

```bash
chmod 400 ~/.ssh/aws-keys.pem
```

Verify that the keys are valids :

```bash
aws ec2 describe-key-pairs --key-name _nameDesired_
```

If needed, we can delete them :

```bash
aws ec2 delete-key-pairs --key-name _nameDesired_
```

#### Create an AMI Role

Fist, create a new role :



## Amazon EC2 Container Service

This part describe the basics commands and options available using the CLI.

### Cluster creation

First, we need to create a new cluster, use the CLI :

```bash
aws ecs create-cluster --cluster-name cluster-name
```

Once create, the cluster is visible in the ECS part of the web interface or via :

```bash
aws ecs list-clusters
```

If needed, more details about a cluster can be found using the CLI :

```bash
aws ecs describe-clusters --cluster clusterName
```

If needed, the cluster can be deleted using the CLI :

```bash
aws ecs delete-cluster clusterName
```

### Container creation



## Examples

[Basic cluster](AWS/basic.md)

[Advanced cluster](AWS/advanced.md)

[Fault tolerant cluster](AWS/fault_tolerant.md)
