


AWS Cloudtrail logs the AWS API activities from Console, SDK, CLI and AWS Services eg. create Bucket, launch EC2 etc.
CloudTrail EventLLogs has
* CloudTrail Manaement Events -> Create VPC, Create S3 Bucket...
* CloudTrail Data Events -> Get S3 Objects, List S3 Objects...



AWS Config manages rules which define a set of desired configuration settings. The pre-built AWS rules (over 75) evaluate provisioning and configuring of AWS resources. 
eg. Ensure Lambda functions are deployed inside a VPC, Enable backups for RDS DB instances, Disable public read for S3 bucket

 
AWS GuardDuty is a MACHINE LEARNING based anomaly and threat detection service to identify suspicious activity, such as unauthorized access attempts and malicious IP addresses. It monitors
* CloudTrail EventLogs, 
* VPC Flow Logs
* DNS Logs
* Kubernetes Audit Logs
Can protect against CryptoCurrency attacks (has a dedicated “finding” for it)



Amazon Inspector only evaluates EC2 instances, Container Images & Lambda functions for software vulnerabilities (against database of CVE) and unintended network exposure.


Security Hub is a central security tool which aggregrates alerts from other Security Tools like GuardDuty, Inspector, Macie, IAM Access Analyzer, AWS Systems Manager, AWS Firewall Manager, AWS Partner Network Solutions
We must first enable the AWS Config Service to use Security Hub
When setting up Security Hub, we must enable/disable security standards like: 
* CIS AWS Foundations,
* PCI DSS
* AWS Foundational Security Best Practices



AWS Detective provides investigative process with prebuilt data aggregations, summaries, and context for DEEP root cause analysis
It atomatically collects and processes events from VPC Flow Logs, CloudTrail, and GuardDuty to create a unified view


AWS Trusted Advisor analyses your AWS account and provides recommendations for
1. Cost Optimization: eg. low utilization EC2 instances, idle load balancers, under-utilized EBS volumes… , Reserved instances & savings plans optimizations, 
2. Performance: eg High utilization EC2 instances, CloudFront CDN optimizations, EC2 to EBS throughput optimizations, Alias records recommendations
3. Security: MFA enabled on Root Account, IAM key rotation, exposed Access Keys, S3 Bucket Permissions for public access, security groups with unrestricted ports 
4. Fault Tolerance: EBS snapshots age, Availability Zone Balance, ASG Multi-AZ, RDS Multi-AZ, ELB configuration… 
5. Service Limits


Penetration Testing on AWS Cloud
AWS customers are welcome to carry out security assessments or penetration tests against their AWS infrastructure without prior approval for 8 services:
• Amazon EC2 instances, NAT Gateways, and Elastic Load Balancers
• Amazon RDS
• Amazon CloudFront
• Amazon Aurora
• Amazon API Gateways
• AWS Lambda and Lambda Edge functions
• Amazon Lightsail resources
• Amazon Elastic Beanstalk environments

Prohibited Activities
• DNS zone walking via Amazon Route 53 Hosted Zones
• Denial of Service (DoS), Distributed Denial of Service (DDoS), Simulated DoS, Simulated DDoS
• Port flooding
• Protocol flooding
• Request flooding (login request flooding, API request flooding)





AWS Audit Manager maps your compliance requirements to AWS usage data with prebuilt and custom frameworks and automated evidence collection to generate compliance reports alongside evidence folders. Prebuilt Feameworks include
* CIS AWS Foundations Benchmark 1.2.0 & 1.3.0
* General Data Protection Regulation (GDPR),
* Health Insurance Portability and Accountability Act (HIPAA)
* Payment Card Industry Data Security Standard (PCI DSS) v3.2.1
* Service Organization Control 2 (SOC 2)




VPC Flow Logs capture information about IP traffic going into interfaces (to either Cloudwatch or S3) at either
* VPC Level
* Subnet Level
* Elastic Network Interface (ENI) level

VPC Flow Logs default syntax
{version} {account-id} {interface-id} {srcaddr} {dstaddr} {srcport} {dstport} {protocol} {packets} {len-bytes} {start} {env} {action} {log-status}

VPC Flow Logs - The following traffic is NOT CAPTURED
• Traffic to Amazon DNS server (custom DNS server traffic is logged)
• Traffic for Amazon Windows license activation
• Traffic to and from 169.254.169.254 for EC2 instance metadata
• Traffic to and from 169.254.169.123 for Amazon Time Sync service
• DHCP traffic
• Mirrored traffic
• Traffic to the VPC router reserved IP address (e.g., 10.0.0.1)
• Traffic between VPC Endpoint ENI and Network Load Balancer ENI



AWS Macie Used to analyze and identify sensitive data in your S3 buckets usin
1. Managed Data Identifier - > A set of built-in criteria that are designed to detect specific type of sensitive data e.g. credit cards numbers, AWS Credentials, bank accounts
2. Custom Data Identifier -> A set of criteria that you define to detect sensitive data using Regular expression, keywords eg. employee IDs, customer account numbers
You can use Allow Lists to define a text pattern to ignore (e.g., public phone numbers)



Unified CloudWatch Agent
Collect additional system-level metrics such as RAM, processes, used disk space, etc from EC2 instances, on-premises servers, …)
No logs from inside your EC2 instance will be sent to CloudWatch Logs without using an agent





Amazon Athena – Federated Query allows you to run SQL queries across data stored in relational, non-relational, object, and custom data sources (AWS or on-premises). It uses Data Source Connectors that run on AWS Lambda to run Federated Queries (e.g., CloudWatch Logs, DynamoDB, RDS, …) and stores the results back in Amazon S3.




AWS Site to Site VPN connects AWS VPC to Customer On-Premise VPC using
1. Virtual Private Gateway(VGW) is created and attached to the AWS VPC from which you want to create the Site-to-Site VPN connection
2. Customer Gateway (CGW) is Software application or physical device on customer side of the VPN connection


Route Propagation or VPG must be ENABLED in the route table associated with your subnets



AWS VPN CloudHub

Customer networks can communicate with each other also, if connected to the same VGW
We need to enable dynamic routing and configure route tables



AWS S3 Access Points simplify security management for S3 Buckets, 
Each access point has
1. its own DNS name (Internet Origin or VPC Origin)
2. an access point policy (similar to bucket policy) – manage security at scale


1. If using VPC Endpoint, we must enable VPC Endpoint to access Access Point via Endpoint Policy
2. When using S3 Access Point, we can enable all S3 API calls to use Access Point only, hence enforcing VPC Endpoints to interact with S3 bucket
