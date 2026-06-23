# Build-a-AWS-Virtual-Private-Cloud-VPC

## Overview
This project demonstrates how to build a Virtual Private Cloud (VPC) on Amazon Web Services (AWS). 
A VPC is a virtual network that allows you to launch AWS resources in a logically isolated section of the AWS cloud. 
It provides control over your network configuration, including IP address ranges, subnets, route tables, and network gateways.

## Services Used
- Amazon VPC
- Subnets
- Route Tables
- Internet Gateway
- Security Groups
- Network Access Control Lists (NACLs)
- EC2 Instances
- Load Balancers
- NAT Gateways

## Architecture
![Architecture Diagram](architecture-diagram.png)

## Steps

1. Create a VPC
- create a new VPC with a specified CIDR block (e.g., 10.0.0.0/16).
- Create 1 public subnet and 1 private subnet in different availability zones "us-east-1a" and "us-east-1b".
- Create an Internet Gateway and attach it to the VPC.
- Create a Route Table and associate it with the public subnet and 2 Route Table one each for the private subnets.
- Create a NAT Gateway in the public subnet to allow instances in the private subnet to access the internet.

![Architecture Diagram](screenshots/vpc-1.png)
![Architecture Diagram](screenshots/vpc-2.png)

 
2. Create auto scaling group
- Launch template configuration for the EC2 instances in the private subnet.
- create a security group for the EC2 instances to allow inbound traffic on port 8000 (HTTP) and port 22 (SSH).

![Architecture Diagram](screenshots/security-groups.png)

- Create an Auto Scaling Group (ASG) with  a desired capacity of 2 instances with a minimum of 2 instances and a maximum of 4 instances.

![Architecture Diagram](screenshots/group-size-scaling.png)

- One instance will be launched in the us-east-1a availability zone and the other instance will be launched in the us-east-1b availability zone.

![Architecture Diagram](screenshots/az-instances.png)


3. Create bastion host
- Now create a bastion host instances in the public subnet to allow SSH access to the instances in the private subnet. 
- In "Network settings" section, select the right VPC and public subnet, and assign (enable Auto-assign public IP) a public IP address to the bastion host instance.
- Create a security group for the bastion host instance to allow inbound SSH traffic.

![Architecture Diagram](screenshots/bastion-host.png)



```bash
You can use the following command to connect to the bastion host instance using SSH:
ssh -i /path/to/your-key.pem username@bastion-public-ip

You can use the following command to copy files like key name pair from your local machine to the bastion host instance using SCP:
scp -i /path/to/your-key.pem /path/to/local/file.txt username@ec2-public-ip:/path/to/remote/directory/

```


## Lessons Learned

## Conclusion
