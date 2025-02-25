# AWS
- [Aurora](#aurora)
- [Auto Scaling Group](#auto_scaling_group)
- [EBS Volumes](#ebs_volumes)
- [EC2 User Data](#ec2_user_data)
- [IAM](#iam)
- [IAM Policies](#iam_policies)
- [IAM Roles](#iam_roles)
- [Lambda](#lambda)
- [Lambda layers](#lambda_layers)
- [Load balancer](#load-balancer)
- [RDS](#rds)
- [Regions and Availability Zones](#regions_and_availability_zones)
- [Route 53](#route_53)
- [S3 Pre-signed URL](#s3_pre_signed_url)
- [Security Groups](#security_groups)

## Aurora <a name="aurora"></a>
Aurora is a relational database engine that works similarly to other but has some better features, is faster than classic RDS but is it about 20% more expensive than RDS.
## Auto Scaling Group <a name="auto_scaling_group"></a>
ASG contains a collection of EC2 instances that are automatically launched or terminated based on pre-defined scaling policies. The scaling policies determine when to increase or decrease the number of instances based on metrics such as CPU utilization, network traffic, or custom metrics.

## EBS Volumes <a name="ebs_volumes"></a>
Elastic Block Store (EBS) can be considered a network drive. It allows us to persist data between instances even after EC2 termination.
## EC2 User Data <a name="ec2_user_data"></a>
EC2 User Data is a feature that allows you to pass scripts to an EC2 instance during its launch. When an EC2 instance is launched with user data, it is executed as soon as the instance starts up. 

## IAM <a name="iam"></a>
IAM (Identity and Access Management) is a service that allows you to manage users, groups, roles and access permissions to AWS services and resources. IAM is intended for use within an organization.

## IAM Policies <a name="iam_policies"></a>
Real permissions in JSON format that we can grant to users or groups.

## IAM Roles <a name="iam_roles"></a>
Permissions granted to AWS services, e.g. EC2, Lambda.

## Lambda <a name="lambda"></a>
AWS Lambda scales CPU power in proportion to the memory setting (RAM).

## Lambda layers <a name="lambda_layers"></a>
A Lambda layer is a .zip file archive that contains common code, data or libraries (numpy, pandas etc.). Reasons why you can consider using layers:
- Reduce the size of your deployment packages.
- Separate core function logic from dependencies.
- Share dependencies across multiple functions.

## Load balancer <a name="load_balancer"></a>
Its purpose is to distribute incoming network traffic across multiple targets, such as EC2 instances and containers, in order to improve the availability and scalability of your application.

## RDS <a name="rds"></a>
Relational Database Service it's a managed database service for databases that use SQL. It allows you to create databases in the cloud that are managed by AWS. RDS supports a variety of popular database engines, including Amazon Aurora, PostgreSQL, MySQL, MariaDB, Oracle Database, and Microsoft SQL Server.

## Regions and Availability Zones <a name="regions_and_availability_zones"></a>
Completely separate physical servers/data centers. Served to ensure the lowest possible latency and high availability to the users. Most AWS services are Region-scope.

## Route 53 <a name="route_53"></a>
Route 53 is a service that allows you to register your domain and route traffic to resource other AWS services.

## S3 Pre-signed URL <a name="s3_pre_signed_url"></a>
Temporarily working URL to file in your private S3 bucket

## Security Groups <a name="security_groups"></a>
They control the traffic so what is allowed to go in or out of EC2 Instances.
