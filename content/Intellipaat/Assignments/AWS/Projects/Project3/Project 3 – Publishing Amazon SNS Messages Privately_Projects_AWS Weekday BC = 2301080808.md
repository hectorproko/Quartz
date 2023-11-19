#AWS

> [!info] Project - 3: Publishing Amazon SNS Messages Privately
> **Industry:** Healthcare 
> 
> **Problem Statement:** 
> How to secure patient records online and send it privately to the intended party 
> 
> **Topics:** 
> In this project, you will be working on a hospital project to send reports online and develop a platform so the patients can access the reports via mobile and push notifications. You will publish the report to an Amazon SNS keeping it secure and private. Your message will be hosted on an EC2 instance within your Amazon VPC. By publishing the messages privately, you can improve the message delivery and receipt through Amazon SNS. 
> 
> **Highlights:** 
> 1. AWS CloudFormation to create a VPC 
> 2. Connect VPC with AWS SNS 
> 3. Publish message privately with SNS


%% #question Not sure what the connection of Lambda functions is to the rest of thing s[[Project-3-–-Solution-1.pdf]]%%

To clone the repository that contains the CloudFormation templates, I use the following command and link:
```bash
git clone https://github.com/aws-samples/aws-sns-samples.git
```

%%[[Project-3-–-Solution-1.pdf#page=2&selection=24,0,24,35|Step 1: Create an Amazon EC2 Key Pair:]]
%%
### Step 1: EC2 Key Pair
I have will make usre of a private key I already have
![[Pasted image 20231103143217.png]]


%%[[Project-3-–-Solution-1.pdf#page=3&selection=24,0,24,31|Step 2: Create the AWS Resource]]%%

### Step 2: Create the AWS Resource

> [!NOTE] Template
> [SNS-VPCE-Tutorial-CloudFormation.template](https://github.com/aws-samples/aws-sns-samples/blob/master/templates/SNS-VPCE-Tutorial-CloudFormation.template)
> 
> The provided CloudFormation template defines a set of AWS resources for setting up a VPC and related components for an SNS VPC Endpoints tutorial. Here's a summary of the resources it creates and their purposes:
> 
> 

%%
> [!tip]- Template in detail
> - **Parameters**: Inputs for the SSH key name and the SSH access IP range.
> - **Mappings**: Specifies AMI IDs for different AWS regions.
> - **Resources**:
>     - `VPC`: A virtual private cloud with a CIDR block of `10.0.0.0/16`.
>     - `Subnet`: A subnet within the VPC with a CIDR block of `10.0.0.0/24`.
>     - `InternetGateway`: An internet gateway for connecting the VPC to the internet.
>     - `VPCGatewayAttachment`: Attaches the internet gateway to the VPC.
>     - `RouteTable`: A routing table for network traffic routing within the VPC.
>     - `SubnetRouteTableAssociation`: Associates the subnet with the route table.
>     - `InternetGatewayRoute`: A route in the route table for directing traffic to the internet gateway.
>     - `SecurityGroup`: Security settings for controlling traffic to and from EC2 instances.
>     - `EC2Instance`: An EC2 instance configured with a specified key name and instance type, associated with the created security group and subnet.
>     - `EC2InstanceProfile` and `EC2InstanceRole`: IAM role and profile to grant the EC2 instance necessary permissions.
>     - `LambdaExecutionRole`: An IAM role for Lambda function execution with basic execution permissions.
>     - `LambdaFunction1` and `LambdaFunction2`: Two Lambda functions with code to process SNS messages.
>     - `LambdaPermission1` and `LambdaPermission2`: Permissions for SNS to invoke the Lambda functions.
>     - `LambdaLogGroup1` and `LambdaLogGroup2`: Log groups for the Lambda functions with a retention policy of 7 days.
>     - `SNSTopic`: An SNS topic with subscriptions to the Lambda functions.

%%

I navigate to CloudFormation Dashboard and click "Create stack"

- **Step 1**: Create stack
  ![[Step 1Create stack.png|400]]
  *We upload the template*

- **Step 2**: Specify stack details
  ![[Step 2Specify stack details.png|400]]
  *After naming the stack, I fill in the 'KeyName' parameter with the name of an existing EC2 KeyPair to enable SSH access. I set the 'SSHLocation' parameter to '0.0.0.0/0', which allows SSH connections from any IP address.*

- **Step 3**: Configure stack options
  *Left all options at their default settings.*  

- **Step 4**: Review


%%[[Project-3-–-Solution-1.pdf#page=6&selection=4,0,4,67|Step 3: Confirming the EC2 Instance lacks internet access]]%%
### Step 3: Confirming the EC2 Instance lacks internet access

First, I'll need to establish an SSH connection, it is necessary to obtain the EC2 instance's public IP address.
![[Pasted image 20231103145918.png]]

Using the Public IP I `ssh` into the EC2
![[Pasted image 20231103150221.png]]

Using ping verifies instance's lack of internet connectivity:
![[Pasted image 20231103150323.png]]

To verify that the instance lacks connectivity to Amazon SNS:
![[Pasted image 20231103150832.png|450]]

Using AWS CLI I attempt to publish a message SNS topic `VPCE-Tutorial-Topic`
```bash
aws sns publish --region us-east-1 --topic-arn arn:aws:sns:us-east-1:838427752759:VPCE-Tutorial-Topic --message "Hello"
```
![[Pasted image 20231103151127.png]]
*No message is published*

%%[[Project-3-–-Solution-1.pdf#page=7&selection=42,0,42,52|Step 4: Create an Amazon VPC Endpoint for Amazon SNS]]%%
### Step 4: VPC Endpoint for Amazon SNS

I begin by assigning the endpoint a Name Tag: 'VPCE-Tutorial'. Under **Services**, I select the AWS service that the endpoint will connect to, which is the Simple Notification Service (SNS) in the US East (N. Virginia) region, identified by `com.amazonaws.us-east-1.sns`.
![[Pasted image 20231103153253.png]]
I ensure that I select the VPC that was created from the CloudFormation template.
![[Pasted image 20231103153311.png]]
![[Pasted image 20231103153517.png]]
I select the 'Tutorial Security Group' as the Security Group, which was previously established by the CloudFormation template.
![[Pasted image 20231103153433.png]]

![[endpoint vpce-tutorial.png]]


%%[[Project-3-–-Solution-1.pdf#page=10&selection=4,0,4,50|Step 5: Publish a message to your Amazon SNS topic]]%%
### Step 5: Publish a message to SNS topic

[[Pasted image 20231103151127.png|Once again]], I use the AWS CLI to publish a message to the SNS topic `VPCE-Tutorial-Topic`.
```bash
aws sns publish --region us-east-1 --topic-arn arn:aws:sns:us-east-1:838427752759:VPCE-Tutorial-Topic --message "Hello"
```
![[Pasted image 20231103153954.png]]


%%[[Project-3-–-Solution-1.pdf#page=10&selection=22,0,22,38|Step 6: Verify your message deliveries]]%%
### Step 6: Message deliveries verification

To verify that the Lambda functions were invoked
%%[[VPCE-Tutorial-Lambda-1.png]]%%
![[Pasted image 20231103154701.png|300]]

To verify that the CloudWatch logs were updated:

> [!NOTE] VPCE-Tutorial-Lambda-1
> ![[VPCE-Tutorial-Lambda-1 cloudwatch.png]]
> 
> > [!success]
> > ![[Pasted image 20231103155309.png]]
> 

> [!NOTE] VPCE-Tutorial-Lambda-2
> 
> ![[Pasted image 20231103155506.png]]
> 
> 
> > [!success]
> > ![[Pasted image 20231103155525.png]]
> 
> 

%%[[Project-3-–-Solution-1.pdf#page=12&selection=24,0,24,16|Step 7: Clean Up]]%%

### Step 7: Clean Up

To delete the VPC endpoint: 
I go to `Actions > Delete VPC endpoints`
![[endpoint vpce-tutorial.png]]


To delete the AWS CloudFormation stack:
![[Pasted image 20231103160118.png|500]]

