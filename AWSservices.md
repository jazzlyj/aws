Module 1:

[Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2/) provides secure, resizable compute capacity in the cloud as Amazon EC2 instances. 

Amazon EC2 Auto Scaling.

**Elastic Load Balancing** - automatically distributes incoming application traffic across multiple resources, such as Amazon EC2 instances.

Elastic Load Balancing and Amazon EC2 Auto Scaling are separate services, they work together to help ensure that applications running in Amazon EC2 can provide high performance and availability. 

In a microservices approach, application components are loosely coupled

**Amazon Simple Notification Service (Amazon SNS)** is a publish/subscribe service. Using Amazon SNS topics, a publisher publishes messages to subscribers.

**Amazon Simple Queue Service (Amazon SQS)** is a message queuing service. 

Using Amazon SQS, you can send, store, and receive messages between software components, without losing messages or requiring other services to be available

Module 2:

The term “serverless” means that your code runs on servers, but you do not need to provision or manage these servers. 

[**AWS Lambda**](https://aws.amazon.com/lambda) is a service that lets you run code without needing to provision or manage servers. 

While using AWS Lambda, you pay only for the compute time that you consume. Charges apply only when your code is running. 

**Containers** provide you with a standard way to package your application's code and dependencies into a single object. You can also use containers for processes and workflows in which there are essential requirements for security, reliability, and scalability.

Container orchestration services help you to deploy, manage, and scale your containerized applications. Two services provide container orchestration: 

Amazon Elastic Container Service and ECS

Amazon Elastic Kubernetes Service. EKS


Module 3:

- AWS Regions and Availability Zones
- Edge locations and Amazon CloudFront
- The AWS Management Console, AWS CLI, and SDKs
- AWS Elastic Beanstalk
- AWS CloudFormation

A Region = general geographic location of availability zones

4 key factors to choose a Region: Compliance, proximity, feature availability, and pricing

An **Availability Zone** is a single data center or a group of data centers within a Region

Content Deliver Network CDN -  Amazon CloudFront.

An **edge location** is a site that **Amazon CloudFront** uses to store cached copies of your content closer to your customers for faster delivery. 

AWS Provisioning – through Web Console, CLI or SDKs

**AWS Elastic Beanstalk**, you provide code and configuration settings, and Elastic Beanstalk deploys the resources necessary to perform the following tasks:

- Adjust capacity
- Load balancing
- Automatic scaling
- Application health monitoring

**AWS CloudFormation**, you can treat your infrastructure as code. This means that you can build an environment by writing lines of code

*best practice*, always deploy infrastructure across at least two Availability Zones. 

some AWS services like Elastic Load Balancing, Amazon SQS, and Amazon SNS already do this for you






Module 4:

Amazon VPC an isolated section of AWS Cloud. Within a virtual private cloud (VPC), you can organize into subnets. A **subnet** is a section of a VPC that contains specific isolatable resources like EC2 instances.

To allow public traffic from the internet to access your VPC, you attach an **internet gateway** 

**virtual private gateway** to establish a virtual private network (VPN) connection between your VPC and a private network, ie on-premises data center or internal corporate network.

[**AWS Direct Connect**](https://aws.amazon.com/directconnect/) is a service that enables you to establish a dedicated private connection between your data center and a VPC.  

The VPC component that checks packet permissions for subnets is a [**network access control list (ACL)**](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html).

**Network access control lists (ACLs)**

A network access control list (ACL) is a virtual firewall that controls inbound and outbound traffic at the subnet level. By default, your account’s default network ACL allows all inbound and outbound traffic

**Stateless packet filtering**

Network ACLs perform **stateless** packet filtering. They remember nothing and check packets that cross the subnet border each way: inbound and outbound. 

**Security groups**

A security group is a virtual firewall that controls inbound and outbound traffic for an Amazon EC2 instance.

By default, a security group denies all inbound traffic and allows all outbound traffic.

**Stateful packet filtering**

Security groups perform **stateful** packet filtering. They remember previous decisions made for incoming packets.

[**Amazon Route 53**](https://aws.amazon.com/route53) is a DNS web service. register new domain names directly in Route 53.

Amazon Route 53 uses DNS resolution to identify AnyCompany.com’s corresponding IP address, 192.0.2.0. This information is sent back to the customer. The customer’s request is sent to the nearest edge location through Amazon CloudFront. Amazon CloudFront connects to the Application Load Balancer, which sends the incoming packet to an Amazon EC2 instance.






Module 5:

volumes behave like physical hard drives

An [**instance store**](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) provides temporary block-level storage for an Amazon EC2 instance.

An instance store is disk storage that is physically attached to the host computer for an EC2 instance, and therefore has the same lifespan as the instance. use cases that involve temporary data that you do not need in the long term

[**Amazon Elastic Block Store (Amazon EBS)**](https://aws.amazon.com/ebs) is a service that provides block-level storage.

Persistent storage. If you stop or terminate an Amazon EC2 instance, all the data on the attached EBS volume remains available. 

An [**EBS snapshot**](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSSnapshots.html) is an incremental backup


In **object storage**, each object consists of data, metadata, and a key.

when you modify a file in block storage, only the pieces that are changed are updated. When a file in object storage is modified, the entire object is updated.

[**Amazon Simple Storage Service (Amazon S3)**](https://aws.amazon.com/s3/) is a service that provides object-level storage. Amazon S3 stores data as objects in buckets

Amazon S3 storage class, consider these two factors:

- How often you plan to retrieve your data
- How available you need your data to be


Storage classes:

S3 Standard

- Designed for frequently accessed data
- Stores data in a minimum of three Availability Zones

S3 Standard-Infrequent Access (S3 Standard-IA)

- Ideal for infrequently accessed data
- Similar to S3 Standard but has a lower storage price and higher retrieval price

S3 One Zone-Infrequent Access (S3 One Zone-IA)

S3 Intelligent-Tiering

S3 Glacier

- Low-cost storage designed for data archiving
- Able to retrieve objects within a few minutes to hours

S3 Glacier Deep Archive

**EBS vs S3**

if you are using complete objects or only occasional changes, S3 

doing complex read, write, change functions, then, EBS

In **file storage**, multiple clients (such as users, applications, servers, and so on) can access data that is stored in shared file folders. In this approach, a storage server uses block storage with a local file system to organize files.

Compared to block storage and object storage, file storage is ideal for use cases in which a large number of services and resources need to access the same data at the same time

[**Amazon Elastic File System (Amazon EFS)**](https://aws.amazon.com/efs/) is a scalable file system used with AWS Cloud services and on-premises resources. As you add and remove files, Amazon EFS grows and shrinks automatically. It can scale on demand to petabytes without disrupting applications.

**EBS vs EFS**

An Amazon EBS volume stores data in a **single** Availability Zone. 

To attach an Amazon EC2 instance to an EBS volume, both the Amazon EC2 instance and the EBS volume must reside within the same Availability Zone.

Amazon EFS is a regional service. It stores data in and across **multiple** Availability Zones. 




The duplicate storage enables you to access data concurrently from all the Availability Zones in the Region where a file system is located. Additionally, on-premises servers can access Amazon EFS using AWS Direct Connect.

[**Amazon Relational Database Service (Amazon RDS)**](https://aws.amazon.com/rds/)  *relational databases* in the AWS Cloud.

Amazon RDS is a managed service that automates tasks such as hardware provisioning, database setup, patching, and backups. 

Amazon RDS is available on six database engines, which optimize for memory, performance, or input/output (I/O). 

[**Amazon Aurora**](https://aws.amazon.com/rds/aurora/) is an *enterprise-class relational database*. It is compatible with MySQL and PostgreSQL relational databases. It is up to five times faster than standard MySQL databases and up to three times faster than standard PostgreSQL databases.

Consider Amazon Aurora if your workloads require high availability. It replicates six copies of your data across three Availability Zones and continuously backs up your data to Amazon S3.

**Nonrelational databases**

“NoSQL databases” because they use structures other than rows and columns to organize data. One type of structural approach for nonrelational databases is key-value pairs.

In a key-value database, you can add or remove attributes from items in the table at any time. Additionally, not every item in the table has to have the same attributes. 

[**Amazon DynamoDB**](https://aws.amazon.com/dynamodb/) is a *key-value database* service. It delivers single-digit millisecond performance at any scale.

DynamoDB is:

- Serverless - do not have to provision, patch, or manage servers.  do not have to install, maintain, or operate software.
- Automatic scaling - As the size of your database shrinks or grows, DynamoDB automatically scales to adjust for changes in capacity while maintaining consistent performance.  suitable choice for use cases that require high performance while scaling.

**Data warehousing**

[**Amazon Redshift**](https://aws.amazon.com/redshift) is a *data warehousing* service that you can use for big data analytics. It offers the ability to collect data from many sources and helps you to understand relationships and trends across your data.


Module 6: SECURITY

Shared Responsibility Model:

- AWS is responsible for the security of the cloud.
- you are responsible for the security in the cloud. 

[**AWS Identity and Access Management (IAM)**](https://aws.amazon.com/iam/)  manage access to AWS services and resources securely.  

Create an account, creates root user. Suggested to activate MFA

- IAM user: (a person or an app) by default has NO permissions. *least privilege principle*
- IAM polices:  a document that allows or denies permissions to AWS services and resources.  IAM policies enable you to customize users’ levels of access to resources
  - Eg: allowing specific actions within Amazon S3: ListObject and GetObject. The policy also mentions a specific bucket ID: *awsdoc-example-bucket*.

- IAM group: a collection of IAM users. assign an IAM policy to a group, all users in the group are granted permissions specified by the policy.
- IAM roles: an identity that you can assume to gain temporary access to permissions, such as switching to different tasks to be performed temporarily. someone assumes an IAM role, they abandon all previous permissions that they had under a previous role and assume the permissions of the new role

MFA

[**AWS Organizations](https://aws.amazon.com/organizations)** to consolidate and manage multiple AWS accounts within a central location

centrally control permissions for the accounts in your organization by using [**service control policies (SCPs)**](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html). SCPs enable restrictions on the AWS services, resources, and individual API actions that users and roles in each account can access.

you can group accounts into organizational units (OUs) to make it easier to manage accounts with similar business or security requirements.

[**AWS Artifact**](https://aws.amazon.com/artifact)  service provides on-demand access to AWS security and compliance reports and select online agreements. AWS Artifact consists two sections: AWS Artifact Agreements and AWS Artifact Reports.

A denial-of-service (DoS) attack - a deliberate attempt to make a website or application unavailable to users

distributed denial-of-service (DDoS) attack, multiple sources are used to start an attack that aims to make a website or application unavailable.

**AWS Shield** protects applications against DDoS attacks. Standard (no cost) and Advanced (paid). integrates with other services such as Amazon CloudFront, Amazon Route 53, and Elastic Load Balancing

applications’ data is secure while in storage **(encryption at rest)** and while it is transmitted, known as **encryption in transit**.

**AWS Key Management Service (AWS KMS)**

perform encryption operations through the use of **cryptographic keys**

[**AWS WAF**](https://aws.amazon.com/waf) is a web application firewall; monitor network requests that come into your web applications

**Amazon Inspector** improve the security and compliance of applications by running automated security assessment

[**Amazon GuardDuty**](https://aws.amazon.com/guardduty)  provides intelligent threat detection for your AWS infrastructure and resources. It identifies threats by continuously monitoring the network activity and account behavior


Module 7: Monitoring and Analytics

[**Amazon CloudWatch**](https://aws.amazon.com/cloudwatch/) monitor and manage various metrics and configure alarm actions based on data from those metrics

CloudWatch uses [**metrics**](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) to represent the data points for your resources.

create [**alarms**](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) that automatically perform actions if the value of your metric has gone above or below a predefined threshold.

CloudWatch [**dashboard**](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Dashboards.html) feature - access all the metrics for your resources from a single location

[**AWS CloudTrail**](https://aws.amazon.com/cloudtrail/) records API calls for your account. 

includes the identity of the API caller, the time of the API call, the source IP address of the API caller, and more. 

` `[**CloudTrail Insights**](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-insights-events-with-cloudtrail.html). This optional feature to automatically detect unusual API activities in your AWS account

[**AWS Trusted Advisor**](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/)  inspects your AWS environment and provides real-time recommendations in accordance with AWS best practices. Checks 5 categories: 

cost optimization, performance, security, fault tolerance, and service limits.

Module 8: Pricing and Support

**AWS Free Tier**

[AWS Free Tier](https://aws.amazon.com/free/)  certain services without incurring costs for the specified period. 

3 types available: 

- Always Free
- 12 Months Free
- Trials

**How AWS pricing works**

- Pay for what you use
- Pay less when you reserve
- Pay less with volume-based discounts when you use more

[**AWS Pricing Calculator**](https://calculator.aws/#/)  create an estimate for the cost of your use cases on AWS

Examples:

**AWS Lambda** 

charged based on the number of requests for your functions and the time that it takes for them to run.

AWS Lambda allows 1 million free requests and up to 3.2 million seconds of compute time per month.

**Amazon EC2**

` `only the compute time that you use while your instances are running

**Amazon S3**

- **Storage -**  pay for only the storage that you use. charged the rate to store objects in your Amazon S3 buckets based on your objects’ sizes, storage classes, and how long you have stored each object during the month.
- **Requests and data retrievals -**  pay for requests made to your Amazon S3 objects and buckets. 
- **Data transfer -**  no cost to transfer data between different Amazon S3 buckets or from Amazon S3 to other services within the same AWS Region. pay for data that you transfer into and out of Amazon S3, with a few exceptions. no cost for data transferred into Amazon S3 from the internet or out to Amazon CloudFront. no cost for data transferred out to an Amazon EC2 instance in the same AWS Region as the Amazon S3 bucket.
- **Management and replication -**  pay for the storage management features that you have enabled on your account’s Amazon S3 buckets. These features include Amazon S3 inventory, analytics, and object tagging.

` `[**AWS Billing & Cost Management dashboard**](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html) to pay your AWS bill, monitor your usage, and analyze and control your costs

The consolidated billing feature of AWS Organizations enables you to receive a single bill for all AWS accounts in your organization

[**AWS Budgets**](https://aws.amazon.com/aws-cost-management/aws-budgets), create budgets to plan your service usage, service costs, and instance reservations.

[**AWS Cost Explorer**](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/)  visualize, understand, and manage your AWS costs and usage over time

four different [**Support plans**](https://aws.amazon.com/premiumsupport/plans/) to troubleshoot issues, lower costs, and efficiently use AWS services. 

You can choose from the following Support plans to meet your company’s needs: 

- Basic
  - free for all AWS customers. includes access to whitepapers, documentation, and support communities. can contact AWS for billing questions and service limit increases.
  - limited selection of AWS Trusted Advisor checks & Personal Health Dashboard
- Developer
  - Basic + 
  - Best practice guidance
  - Client-side diagnostic tools
  - Building-block architecture support, which consists of guidance for how to use AWS offerings, features, and services together
- Business
  - Use-case guidance to identify AWS offerings, features, and services that can best support your specific needs
  - All AWS Trusted Advisor checks
  - Limited support for third-party software, such as common operating systems and application stack components
- Enterprise
  - Application architecture guidance, which is a consultative relationship to support your company’s specific use cases and applications
  - Infrastructure event management: A short-term engagement with AWS Support that helps your company gain a better understanding of your use cases. This also provides your company with architectural and scaling guidance.
  - A Technical Account Manager

Technical Account Manager:

provide guidance, architectural reviews, and ongoing communication with your company as you plan, deploy, and optimize your applications.

[**AWS Marketplace**](https://aws.amazon.com/marketplace) is a digital catalog that includes thousands of software listings from independent software vendors. You can use AWS Marketplace to find, test, and buy software that runs on AWS




Module 9: MIGRATION and INNOVATION

[**AWS Cloud Adoption Framework (AWS CAF)**](https://d1.awsstatic.com/whitepapers/aws_cloud_adoption_framework.pdf) organizes guidance into six areas of focus, called **Perspectives**. Each Perspective addresses distinct responsibilities. The planning process helps the right people across the organization prepare for the changes ahead

In general, the **Business**, **People**, and **Governance** Perspectives focus on business capabilities, whereas the **Platform**, **Security**, and **Operations** Perspectives focus on technical capabilities

**6 strategies for migration**

six of the most common [migration strategies](https://aws.amazon.com/blogs/enterprise-strategy/6-strategies-for-migrating-applications-to-the-cloud/) that you can implement are:

- Rehosting – lift and shift
- Replatforming – lift, tinker, and shift
- Refactoring/re-architecting – writing new code, highest initial cost and human effort
- Repurchasing – ending old licensing agreements and starting with a new product. traditional license to a software-as-a-service model
- Retaining – stuff that could be migrated but might be deprecated soon
- Retiring – some parts are just not needed or used

The [**AWS Snow Family**](https://aws.amazon.com/snow) is a collection of physical devices that help to physically transport up to exabytes of data into and out of AWS

Innovate with AWS services:

**SageMaker**, you can quickly and easily begin working on machine learning projects. You do not need to follow the traditional process of manually bringing together separate tools and workflows.

**Textract** is a machine learning service that automatically extracts text and data from scanned documents.

**Lex** is a service that enables you to build conversational interfaces using voice and text.

**DeepRacer** is an autonomous 1/18 scale race car that you can use to test reinforcement learning models.







Module 10: 

[**AWS Well-Architected Framework**](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf) helps you understand how to design and operate reliable, secure, efficient, and cost-effective systems in the AWS Cloud. It provides a way for you to consistently measure your architecture against best practices and design principles and identify areas for improvement

- *Operational excellence*
- *Security*
- *Reliability* - ability of a workload to consistently and correctly perform its intended functions
- *Performance efficiency* - using computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technologies evolve.
- *Cost optimization* - ability to run systems to deliver business value at the lowest price point

**Advantages of cloud computing -** *Six* advantages:

- Trade upfront expense for variable expense.
- Benefit from massive economies of scale.
- Stop guessing capacity.
- Increase speed and agility.
- Stop spending money running and maintaining data centers.
- Go global in minutes.


