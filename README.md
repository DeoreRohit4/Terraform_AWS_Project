# Terraform AWS Infrastructure Project
![terraform](https://github.com/DeoreRohit4/Terraform_AWS_Project/assets/102886808/5ba8ce7a-9002-42fb-8555-3fd569dc2422)

## Overview

This Terraform project demonstrates the creation of a highly available and scalable web application infrastructure on AWS. It provisions a VPC, subnets, an Internet Gateway, route tables, security groups, EC2 instances, an Application Load Balancer (ALB), an S3 bucket, and sets up target group attachments for seamless load balancing across instances. This infrastructure is designed to support a robust web application deployment with emphasis on security, scalability, and high availability across multiple availability zones.

## Architecture

- **VPC**: A Virtual Private Cloud (VPC) with a configurable CIDR block to provide a logically isolated section of the AWS cloud where AWS resources can be launched in a defined virtual network.
- **Subnets**: Two subnets are created across two availability zones (`us-east-1a` and `us-east-1b`) for high availability, each with a CIDR block allowing for public IP address assignment on instance launch.
- **Internet Gateway (IGW)**: Attached to the VPC to enable communication between resources in your VPC and the internet.
- **Route Tables & Associations**: A route table containing a route to the internet via the IGW is created and associated with both subnets, enabling internet access for resources within the subnets.
- **Security Group**: A security group acting as a virtual firewall for EC2 instances to control inbound and outbound traffic. Configured to allow HTTP (port 80) and SSH (port 22) ingress traffic from any IP address, and allow all outbound traffic.
- **EC2 Instances**: Two t2.micro instances are provisioned in each subnet, with user data scripts for initial setup, and attached to the VPC's security group for network security.
- **S3 Bucket**: An S3 bucket named `rohitsterraform2024project` for storage purposes.
- **Application Load Balancer (ALB)**: An ALB to distribute incoming HTTP traffic across the two EC2 instances across different availability zones for high availability. It is associated with the security group and the two subnets.
- **Target Group & Attachments**: A target group for the ALB to route requests to registered targets (EC2 instances) in the specified VPC. Each EC2 instance is registered with the target group.
- **Listener**: A listener for the ALB that checks for incoming connection requests based on the protocol and port you configure (HTTP on port 80) and forwards it to a target group.

## Deployment Steps

1. **Pre-requisites**: Ensure you have Terraform installed and AWS CLI configured with the necessary permissions.
2. **Initialization**: Navigate to the project directory and run `terraform init` to initialize a Terraform working directory.
3. **Plan**: Execute `terraform plan` to preview the actions Terraform will perform based on the configuration files.
4. **Apply**: Apply the changes with `terraform apply` to create the resources on AWS as defined in the Terraform configuration files.
5. **Verification**: After successful application, verify the infrastructure through the AWS Management Console or Terraform outputs, such as the ALB DNS name output to access the web application.

## Outputs

- **loadbalancerdns**: The DNS name of the Application Load Balancer which can be used to access the deployed web application.

## Cleanup

To remove the provisioned infrastructure, run `terraform destroy` and confirm the deletion. This ensures that you are not charged for resources that you no longer use.

## Notes

- Ensure that the AMI IDs and other configurations such as CIDR blocks, instance types, and availability zones are updated according to your requirements.
- Review and adjust the security group rules based on the least privilege principle, allowing only necessary traffic to your instances.
