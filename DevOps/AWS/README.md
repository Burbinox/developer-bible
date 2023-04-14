# AWS
- [Auto Scaling Group](#auto-scaling-group)
- [EBS Volumes](#ebs_volumes)
- [EC2 User Data](#ec2_user_data)
- [IAM](#iam)
- [IAM Policies](#iam_policies)
- [IAM Roles](#iam_roles)
- [Load balancer](#load-balancer)
- [Regions and Availability Zones](#regions_and_availability_zones)
- [Security Groups](#security_groups)

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

## Load balancer <a name="load_balancer"></a>
Its purpose is to distribute incoming network traffic across multiple targets, such as EC2 instances and containers, in order to improve the availability and scalability of your application.

## Regions and Availability Zones <a name="regions_and_availability_zones"></a>
Completely separate physical servers/data centers. Served to ensure the lowest possible latency and high availability to the users. Most AWS services are Region-scope.

## Security Groups <a name="security_groups"></a>
They control the traffic so what is allowed to go in or out of EC2 Instances.
