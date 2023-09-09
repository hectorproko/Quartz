Elastic Compute Cloud
E and 2 Cs

Computing capacity that is scalable

# Features of EC2
- Instances are virtual computing environents.
- Amazon Machine Images (AMIs) are preconfigured templates for your instances that package the bits you need for your server (including the operating system and additional software)
- Instance types are different configurations of CPU, memory, storage, and networking capacity for your instances.
- Using key pairs, you can secure login information for your instances (AWS stores the public key, and you store the private key in a secure place)


# EC2 Pricing
![[Pasted image 20230821193144.png]]
![[Pasted image 20230821193632.png]]
## Free Tier Eligibility
- If you are under the free tier eligibility, you get 750 hours of usage on a t2.micro EC2 instance at no cost.

## Standard Instances
- For other instance types, like `m5.large`, the cost is $0.096 per hour.

## Data Transfer
- Data transfer into the machine is free.
- Data transfer within the same region to services like S3, Glacier, DynamoDB, SQS, SES is also free.
- If the data transfer is to services in a different region, you'll incur additional costs.

## Elastic IPs
- If you're using an Elastic IP, additional charges apply.

## Service Level Agreement (SLA)
- EC2 instances have a 99.99% availability guarantee.

