# Examples

## Setup

vi Dockerfile
```
FROM ruby:alpine3.15

WORKDIR /usr/src/app/
ENV AWS_REGION=eu-central-1

RUN apk --update add --no-cache --virtual run-dependencies \
        terraform \
        aws-cli

RUN gem install terraforming
```


Build image
```
docker build -t terraforming:1.0 .
```


Run Image
```
docker run -it terraforming:1.0 sh
```


Installed Tools in image
- terraform
- terraforming
- aws


## Usage

Show help
```
terraforming

Commands:
  terraforming alb             # ALB
  terraforming asg             # AutoScaling Group
  terraforming cwa             # CloudWatch Alarm
  terraforming dbpg            # Database Parameter Group
  terraforming dbsg            # Database Security Group
  terraforming dbsn            # Database Subnet Group
  terraforming ddb             # DynamoDB
  terraforming ec2             # EC2
  terraforming ecc             # ElastiCache Cluster
  terraforming ecsn            # ElastiCache Subnet Group
  terraforming efs             # EFS File System
  terraforming eip             # EIP
  terraforming elb             # ELB
  terraforming help [COMMAND]  # Describe available commands or one specific command
  terraforming iamg            # IAM Group
  terraforming iamgm           # IAM Group Membership
  terraforming iamgp           # IAM Group Policy
  terraforming iamip           # IAM Instance Profile
  terraforming iamp            # IAM Policy
  terraforming iampa           # IAM Policy Attachment
  terraforming iamr            # IAM Role
  terraforming iamrp           # IAM Role Policy
  terraforming iamu            # IAM User
  terraforming iamup           # IAM User Policy
  terraforming igw             # Internet Gateway
  terraforming kmsa            # KMS Key Alias
  terraforming kmsk            # KMS Key
  terraforming lc              # Launch Configuration
  terraforming nacl            # Network ACL
  terraforming nat             # NAT Gateway
  terraforming nif             # Network Interface
  terraforming r53r            # Route53 Record
  terraforming r53z            # Route53 Hosted Zone
  terraforming rds             # RDS
  terraforming rs              # Redshift
  terraforming rt              # Route Table
  terraforming rta             # Route Table Association
  terraforming s3              # S3
  terraforming sg              # Security Group
  terraforming sn              # Subnet
  terraforming snss            # SNS Subscription
  terraforming snst            # SNS Topic
  terraforming sqs             # SQS
  terraforming vgw             # VPN Gateway
  terraforming vpc             # VPC

Options:
  [--merge=MERGE]                                # tfstate file to merge
  [--overwrite], [--no-overwrite]                # Overwrite existing tfstate
  [--tfstate], [--no-tfstate]                    # Generate tfstate
  [--profile=PROFILE]                            # AWS credentials profile
  [--region=REGION]                              # AWS region
  [--assume=ASSUME]                              # Role ARN to assume
  [--use-bundled-cert], [--no-use-bundled-cert]  # Use the bundled CA certificate from AWS SDK
```



Configure AWS credentials
```
export AWS_ACCESS_KEY_ID="XXXXX"
export AWS_SECRET_ACCESS_KEY="XXXXX"
export AWS_SESSION_TOKEN="XXXXX"
```

Create Terraform code for all EC2 instances
```
terraforming ec2

resource "aws_instance" "terraforming-prod" {
    ami                         = "ami-0358b49d14747474"
    availability_zone           = "eu-central-1b"
    ebs_optimized               = true
    instance_type               = "t3a.medium"
    monitoring                  = false
    key_name                    = ""
    subnet_id                   = "subnet-xxxxxxxxxx"
    vpc_security_group_ids      = ["sg-xxxxxxxxxxxx"]
    associate_public_ip_address = true
    private_ip                  = "192.168.130.100"
    source_dest_check           = true

    root_block_device {
        volume_type           = "gp2"
        volume_size           = 200
        delete_on_termination = true
    }

    tags {
        "Name" = "terraforming-prod"
   
    }
}
```







