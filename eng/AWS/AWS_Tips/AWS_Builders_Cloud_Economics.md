# AWS Builders - Cloud Economics

<br>

## Cloud Financial Management

<br>

### Cost Optimization Big 5

1. Rightsizing

   - Use appropriately sized instances
     - Amazon CloudWatch metrics analysis
     - Cost explorer

2. Scheduling

   - Operate according to usage time

3. Pricing

   - Utilize various pricing policies

     - `On-demand`
       - Pay only for EC2 instances used without commitment
         - As you know, the most expensive.. ㅎ_ㅎ
       - Suitable when traffic is unpredictable

     - `Reserved Instances (RI)`
       - 1 year or 3 year commitment
       - Up to 75% savings compared to on-demand
       - Suitable for consistent/always-on workloads
     - `Savings Plans (SP)`
       - 1 year or 3 year commitment
       - Suitable for consistent/always-on workloads
       - **Details**
         - Flexible pricing model that can save up to 72% on EC2, Fargate and Lambda usage
           - ex) If you commit to $10 for one hour, you use compute resources at discounted hourly rates up to $10
         - Apply discounted Savings Plans rates up to committed usage, beyond that apply `on-demand` rates
       - **Purchase method**
         - Go to AWS Cost Management and you'll find Savings Plans!
     - `Spot Instances`
       - Up to 90% savings compared to on-demand through spare computing capacity
       - For batch workloads without time limits

4. Storage

   - Use various storage classes

5. Monitoring

   - Goal setting and execution 
