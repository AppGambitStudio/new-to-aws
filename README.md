# New To Amazon Web Services (AWS)!!
Nowadays it's very difficult to imagine building an application that does not use any top Cloud providers like AWS, Google Cloud, or Azure. Many fresh or experienced engineers are rushing to learn these cloud services to either upgrade their skillset or build modern applications. 

If you are new to AWS, it can get overwhelming. There are 200+ services and many of them are interdependent and interconnected. I have put a list of core services and concepts that you can refer to and solidify your understanding of the AWS Cloud.

## Purpose
This repo is created for new AWS users to get enough familiarity with the core AWS Cloud services. The focus is on certain critical practices and core services to create a basic mental model that can help the account owners and users to use the AWS cloud safely and effectively.  

Over the years, I have seen many users (Developers or Account Owners) who create AWS accounts for themselves or their team and then quickly find themselves in one or other problems. Having a basic operational understanding of AWS Cloud goes a long way. 

## How to Use this Guide
For each service, I have put some basic explanations, mostly taken from the AWS documentation and other verified sources, and direct links to the documentation pages that the reader will have to go through step by step. 

The AWS documentation is the best source of detailed information. The documentation refererences may feel a bit boring and lengthy, but I have put only the required references that are critical for initial understanding. 

You can stroll around to different resources but do make sure to read through the referenced documentation first.

## FAQ

### Some services start with Amazon and others start with AWS, any reason?
The pattern is that utility services are prefixed with AWS, while standalone services are prefixed by "Amazon".
https://stackoverflow.com/a/33134738/224844

### Is every service chargeable inside AWS? Is there any fixed cost of using AWS?
There are different types of services offered by AWS. Most of the services are charged for the amount of time it is in use, the amount of data being stored or the amount of data being transferred. To simplify, if you create a Virtual Machine using EC2 then you will have to pay for the exact duration the EC2 instance was up and running, even though you didn’t do anything inside but you still have to pay. On the other hand, if you create an S3 storage bucket, but do not store anything inside it then you are not charged for anything because S3 costs for the amount of data that you store and transfer. 

There are a few niche services, like AWS Shield Advanced, that may have fixed monthly costs, but chances are you may not use those services immediately.

However there are different levels of `Free` offerings, Some resources are available free for first 12 months after initial signup, some resources are free for limited duration after you activate them and some resources are free for Life-time. To know more detail, please visit this page. 
https://aws.amazon.com/free/

### Where can I get the latest updates of AWS?
[AWS News](https://aws.amazon.com/new/) is the best source to get the recent features updates, new releases and other related information. 

### Where else I can get more detail resources for AWS?
- https://awsstash.com/
- https://www.youtube.com/watch?v=OQKOHNtyz3E&list=PLhr1KZpdzukdeX8mQ2qO73bg6UKQHYsHb&ab_channel=AmazonWebServices
- https://www.lastweekinaws.com/
- https://www.awsgeek.com/

## Online Courses and Books
- https://www.udemy.com/user/stephane-maarek/
- https://dvassallo.gumroad.com/l/aws-good-parts
- https://acloudguru.com/solutions/individuals
- https://www.whizlabs.com/
- https://www.amazon.com/gp/product/B08HC5T36C/ref=dbs_a_def_rwt_bibl_vppi_i0

## Table of Content
- [AWS Global Infrastructure](#aws-global-infrastructure)
- [AWS Account and Root User](#aws-account-and-root-user)
- [AWS Billing](#aws-billing)
- [Amazon Simple Storage Service (S3)](#amazon-simple-storage-service)
- [Amazon CloudWatch](#amazon-cloudwatch)
- [AWS CloudTrail](#aws-cloudtrail)
- [AWS Virtual Private Cloud (VPC)](#amazon-virtual-private-cloud)
- [Amazon Elastic Compute Cloud (EC2)](#amazon-elastic-compute-cloud-ec2)
- Service quotas
- What’s Free in AWS
- Kill Switch 

![Image](/new-to-aws-image-1.png)

## AWS Global Infrastructure
The AWS Cloud infrastructure is built around AWS Regions, Availability Zones, and Edge locations. An AWS Region is a group of physical locations that has multiple data centers known as Availability Zones. Availability Zones consist of one or more discrete data centers, each with redundant power, networking, and connectivity, housed in separate facilities. These Availability Zones offer you the ability to operate production applications and databases that are more highly available, fault-tolerant, and scalable than would be possible from a single data center.

- https://aws.amazon.com/about-aws/global-infrastructure/
- https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

### Do
- Understand the benefits of having a well-spread global infrastructure
- Select proper geographic location(s) based on the use case of your application

### Don’t
- While following any tutorial, do not create resources in the geographic locations mentioned in that tutorial as it is. I have seen people follow certain regions as it is, because everyone else does that. 


## AWS Account and Root User
When you create an your AWS account, you begin with one identity that has complete access to all the AWS services and resources in the account. This identity is called the AWS account Root User. You can sign in as the root user using the email address and password that you used to create the account.

It is strongly recommended not use the root user for the everyday tasks, even the administrative ones. Instead, adhere to the best practice of using the root user only to create your first IAM user. Then securely lock away the root user credentials and use them to perform only a few account and service management tasks. The IAM user represents the person or service who uses the IAM user to interact with AWS, either through UI or programmatically. The best thing about an IAM user is that, it can only DO things that is explicitly granted, known as Service policies or permissions. 

- https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html
- https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html

### Do
- Enable MFA on Root User
- Create IAM User with specific IAM Permissions
- Create Groups for specific sets of users and Assign Permissions to the Group
- Check permissions of the IAM User before generating and sharing the Access Keys

### Don’t 
- Do not give your Root User Credentials to Anyone
- Do not generate Access Keys for Root User
- Do not generate Access Keys for IAM Users if not needed


## AWS Billing
AWS automatically charges the credit card that you provided when you sign up for an AWS account. You can view or update your credit card information at any time, including designating a different credit card for AWS to charge. Do keep in mind that the charges are only applied if you have used any resources. AWS has highly granular structure for the charges and each service has different and multiple types of charges applied. 

- https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_billing.html
- https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html

AWS Cost Explorer is a tool that enables you to view and analyze your costs and usage. You can explore your usage and costs using the main graph, the Cost Explorer cost and usage reports, or the Cost Explorer RI reports. You can use Cost Explorer to identify areas that need further inquiry and see trends that you can use to understand your costs.

You can use AWS Budgets to track and take action on your AWS cost and usage. You can use AWS Budgets to monitor your aggregate utilization and coverage metrics.

- https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html

### Do
- Create Budget alerts based on your estimated monthly spending
- Give Budget Access Permissions to authorized users only
- Spend a few minutes per month to check your Bill and analyze the resource usage

### Don’t 
- Don’t Assume anything, AWS can be very costly if you do not put guardrails
- Give full permissions to every user that you create in your account


## Amazon Simple Storage Service
Amazon S3 is an object storage service that offers industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can use Amazon S3 to store and protect any amount of data for a range of use cases. Amazon reported it stored more than 100 trillion objects as of [March 2021](https://aws.amazon.com/blogs/aws/amazon-s3s-15th-birthday-it-is-still-day-1-after-5475-days-100-trillion-objects/). Amazon S3 was the earliest cloud service that focused on API-driven Cloud Infrastructure, freeing developers from any capacity planning, pay only for used storage, and with practically unlimited storage capacity. 

Over the years, S3 has kept on adding new innovative features. You can use S3 for the following use cases:
- Privately storing your application data (CSV, Images, Videos, or any other types)
- Static Website Hosting (Angular, Vue, React, or any other JavaScript-based Single Page Applications)
- Store files in different storage formats like Instant Retrieval, Infrequent Retrieval, Long-term backup, etc. Each format has different storage and retrieval cost. 
- Automatically transition stored files to an optimal storage format based on file age, this reduces the storage cost over the period of time.
- Automatically Delete stored files after certain periods of time

`There is nice feature infographic released by AWS after S3 turned 15. It is safe to say, S3 was a pioneer cloud storage service and over the years it transformed the way storage is done and managed.`

https://aws.amazon.com/s3/storage-launches-infographic/

### Refereces
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-bucket-intro.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/aws-billing-reports.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html

### Do
- Depending on your use case, create the Bucket in the same region where the rest of your application resources are running.
- Check your use case and Create Private Buckets Only
- Create Lifecycle policies to transition files to an optimal storage tier
- Create Pre-signed URLs to share files stored in the bucket

### Don’t 
- Do not create Public Buckets unless really required
- Make sure you do not store sensitive user information inside the S3 bucket files unless your application and AWS account has enough security in place. For example, User Personal details, Credit card information, Medical information, etc.


## Amazon CloudWatch
Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real-time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications.

The CloudWatch home page automatically displays metrics about every AWS service you use. You can additionally create custom dashboards to display metrics about your custom applications and display custom collections of metrics that you choose.

With Amazon CloudWatch you can centrally manage your Application Logs, and metrics, configure alarms, and other operational things.

There are interesting things you can do easily with the CloudWatch service. You can install the CloudWatch Agent on your on-prem or another cloud VMs and push logs to CloudWatch Logs, you can create real-time log processing with subscriptions on the logs and invoke Lambda functions or push events to another AWS service.

- https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/GettingStarted.htm
- https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-metrics-basic-detailed.html
- https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html
- https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Subscriptions.html

### Do
- Understand the difference between Log Groups and Log Streams
- Do evaluate what is really needed to be monitored for your application

### Don't
- Enable detail monoting unless required, this will incur additional cost
- Don't do excessive logging, use debug flag or other configs to enable/disable detailed logging in your application

## AWS CloudTrail
AWS CloudTrail helps you enable operational and risk auditing, governance, and compliance of your AWS account. Actions taken by a user, role, or an AWS service are recorded as events in CloudTrail. Events include actions taken in the AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs.

CloudTrail is enabled by default on your AWS account when you create it. When activity occurs in your AWS account, that activity is recorded in a CloudTrail event. You can easily view recent events in the CloudTrail console by going to Event history.

`Note: CloudTrail is one of the most important services in the AWS Cloud. This service will help you log all the AWS API call and enable security analysis, resource change tracking, and compliance auditing.`

- https://docs.aws.amazon.com/awscloudtrail/latest/userguide/how-cloudtrail-works.html
- https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-workflow.html
- https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-and-update-a-trail-by-using-the-console.html

## Amazon Virtual Private Cloud
Amazon Virtual Private Cloud (VPC) gives you full control over your virtual networking environment, including resource placement, connectivity, and security. Many AWS resources can only run inside VPC, like, EC2 Instances, RDS, and Load Balancers. VPC can be internally divided into public and protected sub networks. You can create a public-facing subnet for your web servers that have access to the internet and place your backend systems, such as databases or application servers, in a private-facing subnet with no internet access. Amazon VPC lets you to use multiple layers of security, including security groups and network access control lists, to help control access to Amazon Elastic Compute Cloud (Amazon EC2) instances in each subnet.

Note: When you create a new AWS account, each region has one default VPC created. For many use cases, this default VPC can work just fine. 

- https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html
- https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html
- https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html
- https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-best-practices.html

### Do
- Make sure you use the correct IP CIDR range while creating a new VPC
- Understand the difference between Public and Private Subnets
- Understand the difference between Security Groups and Network Access Control List (NACL)
- Make sure Subnets are not too wide and not too narrow

### Don't
- Don't enable the public SSH access to EC2 instances, use your Home IP (temporary) or specific IP range of you home Internet
- Don't create NAT Gateway unless really required. NAT Gateway has additional cost attached to it.

## Amazon Elastic Compute Cloud (EC2)
First released in 2006, Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing capacity in the Amazon Web Services (AWS) Cloud. You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure security and networking, and manage storage.

Besides Linux and Windows operating systems, in November 2020, Amazon announced that it would be adding macOS to the EC2 service as well. EC2 has a popular Auto scaling feature that allows it to automatically adapt computing capacity to site traffic. 

You can create small EC2 with 2 vCPUs and 0.5GB RAM or very large insntances with 400+ processors and 24TB of RAM. 

As part of the AWS Free Tier, you can get started with Amazon EC2 for free. This includes 750 hours of Linux and Windows t2.micro instances (t3.micro for the regions in which t2.micro is unavailable), each month for one year. To stay within the Free Tier, use only EC2 Micro instances.

Amazon EC2 provides the following features:
- Preconfigured templates for your instances, known as Amazon Machine Images (AMIs), that package the bits you need for your server (including the operating system and additional software)
- Various configurations of CPU, memory, storage, and networking capacity for your instances, known as instance types
- Secure login information for your instances using key pairs (AWS stores the public key, and you store the private key in a secure place)
- Storage volumes for temporary data that's deleted when you stop, hibernate, or terminate your instance, known as instance store volumes
- Persistent storage volumes for your data using Amazon Elastic Block Store (Amazon EBS), known as Amazon EBS volumes
- Multiple physical locations for your resources, such as instances and Amazon EBS volumes, known as Regions and Availability Zones
- A firewall that enables you to specify the protocols, ports, and source IP ranges that can reach your instances using security groups
- Static IPv4 addresses for dynamic cloud computing, known as Elastic IP addresses
- Metadata, known as tags, that you can create and assign to your Amazon EC2 resources
- Virtual networks you can create that are logically isolated from the rest of the AWS Cloud, and that you can optionally connect to your own network, known as virtual private clouds (VPCs)

Amazon EC2 provides the following purchasing options to enable you to optimize your costs based on your needs. If you are still learning EC2, then make sure you always work with On-Demand or Spot instances as they will not incur any fixed cost. 

- On-Demand Instances – Pay, by the second, for the instances that you launch.
- Savings Plans – Reduce your Amazon EC2 costs by making a commitment to a consistent amount of usage, in USD per hour, for a term of 1 or 3 years.
- Reserved Instances – Reduce your Amazon EC2 costs by making a commitment to a consistent instance configuration, including instance type and Region, for a term of 1 or 3 years.
- Spot Instances – Request unused EC2 instances, which can reduce your Amazon EC2 costs significantly.
- Dedicated Hosts – Pay for a physical host that is fully dedicated to running your instances, and bring your existing per-socket, per-core, or per-VM software licenses to reduce costs.
- Dedicated Instances – Pay, by the hour, for instances that run on single-tenant hardware.
- Capacity Reservations – Reserve capacity for your EC2 instances in a specific Availability Zone for any duration.

Amazon EC2 is a complicated service and internally uses many other AWS services. Learning the EC2 and the support services will give you much better understanding of AWS Cloud in general.

- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instances-and-amis.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-group-rules.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring_automated_manual.html
