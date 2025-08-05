# AWS Online Cloud Clinic #1 - 3/4

<br>

<br>

### Collaboration Tools

> Interest in collaboration tools has increased due to increased remote work caused by Coronavirus

- Jandi
- Notion
- Trello

<br>

<br>

## AWS Seoul Region Newly Released Services

<br>

### 1. Launch of Provisioned IOPS `io1` EBS Volume Connectable to Multiple EC2 Instances

- EFS tends to be expensive so you might hesitate, but with the launch of EBS volumes connectable to multiple instances, it seems good to utilize

<br>

### 2. AWS Compute Optimizer

- EC2 has various instance types, but choosing the right instance for your application is not easy
- AWS Compute Optimizer helps optimize this!
- Analyzes your virtual server workloads and tells you which options to use to reduce costs

<br>

### 3. AWS Savings Plans

1. Compute Savings Plans
   - Applicable regardless of region, instance family, size, tenancy, OS
   - Applicable to EC2 instance, AWS Fargate, AWS Lambda service usage
   - Can set hourly commitments
2. EC2 Savings Plans
   - Applicable to committed EC2 family and instance usage within regions regardless of size, tenancy, OS

<br>

<br>

## Q&A

<br>

- Q1) Are there any computing power limitations for Amazon Athena?
  - Athena
    - Serverless data query engine
    - Open Source
  - No computing power limitations
  - Best practices are in AWS Blog
    - ex) Compression etc.

<br>

- Q2) We're planning to build a web service for UK and German users soon. EC2 should obviously be in those regions, but should we also put RDS that was originally managed in US region into UK and German regions? It seems right to separate them, but there's internal opinion to just use US region RDS for management reasons.
  - Basically, it's common to place server and DB server in the same region
  - For European services, there may be personal information storage issues (GDPR), so it's recommended to place RDS in European regions
  - Amazon Aurora has added global database features to address problems, but it's good to choose considering latency issues and security concerns.

<br>

- Q3) We're using DocumentDB in Seoul region - can we expand to other regions because of global service?
  - DocumentDB snapshots cannot yet be copied to other regions
  - Amazon DynamoDB provides global table cross and regional replication
  - Amazon Aurora also provides global data service
  - Other DBs have difficulty supporting global services, so keep this in mind

<br>

<br>

## Tips

- Refer to FAQ within AWS site
  - Materials organized on the site are more extensive and accurate than lectures and books
- Book recommendation
  - Learning and Applying 14 AWS Construction Patterns (translated by Jung Do-hyun, organizer of AWSKRUG Machine Learning Study! I should buy it)
  - <https://brunch.co.kr/@topasvga/666> has AWS-related recommended books organized for reference 
