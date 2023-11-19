==Pending CleanUP==
#AWS

> [!info] Project - 2: Website Orchestration
> **Industry:** Internet related 
> 
> **Problem Statement:** 
> How to orchestrate a website with lesser time and higher availability along with Auto Scaling. 
> 
> **Topics:** 
> In this AWS project, you have to deploy a high-availability PHP application with an external Amazon RDS database to Elastic Beanstalk. Running a DB instance external to Elastic Beanstalk decouples the database from the lifecycle of your environment. This lets you connect to the same database from multiple environments, swap one database for another, or perform a blue/green deployment without affecting your database. 
> 
> **Highlights:** 
> Launch a DB instance in Amazon RDS 
> Create an Elastic Beanstalk Environment 
> Configure Security Groups and Scaling


> [!attention]
> Dear learner,
> 
> I hope this message finds you well. 
> 
> Please be informed that AWS Project 2, involving the PHP application version, has been deprecated due to unsupported PHP version of the application.
> Kindly refrain from attempting this project. 
> 
> Instead, focus your efforts on the remaining projects included in the course. 
> They are designed to provide you with valuable and up-to-date skills. 
> 
> Should you have any questions or need guidance, feel free to reach out to our support team.
> 
> Please share your feedback to make our relationship stronger.


Will use RDS database from [[Project 1 – Deploying A Multi-Tier Website Using AWS EC2_Projects_AWS Weekday BC = 2301080808|Project 1 – Deploying A Multi-Tier Website Using AWS EC2]]

Create a New Elastic Beanstalk Environment just like in [[Assignment 2 – Elastic Beanstalk_Module9_AWS Weekday BC = 2301080808#Step 1 Create a New Elastic Beanstalk Environment|Assignment 2 – Elastic Beanstalk]]


- Step 3 _- optional_
    Set up networking, database, and tags
![[Pasted image 20231102133001.png]]


- Step 4 _- optional_
    Configure instance traffic and scaling

This time added "Auto scaling group"
![[Pasted image 20231101161420.png]]

- Step 5 _- optional_
    Configure updates, monitoring, and logging
Changed it to Apache
![[Pasted image 20231102115746.png]]

![[Pasted image 20231101162647.png]]


%%
# Issue

> [!fail] Beanstalk app doesnt work on my custom VPC `MyVPC`
> 
> 
> > [!question]
> > Potential issue found:
> > ![[Pasted image 20231102110129.png]]
> > one of the private subnets was not connected to a NAT
> 
> > [!success]
> > Worked
> > Changing route table of subnet to lead it to NAT
> > ![[Pasted image 20231102114247.png]]

%%

^6aff71


Issue:

```
|November 2, 2023 14:20:16 (UTC-4)|ERROR|Stack named 'awseb-e-z9v2xmkciy-stack' aborted operation. Current state: 'CREATE_FAILED' Reason: The following resource(s) failed to create: [AWSEBV2LoadBalancer, AWSEBInstanceLaunchWaitCondition].|
```

I think beanstalk doesnt have the right permissions
added "AmazonEC2FullAccess" to role in the EC2 Instance profile
![[Pasted image 20231102144104.png]]
did not work

Trying, which is servie role not profile
''aws-elasticbeanstalk-service-role''

New errror
```
|ERROR|
Creating load balancer failed Reason: 
Resource handler returned message: "At least two subnets in two different Availability Zones must be specified 
(Service: ElasticLoadBalancingV2, Status Code: 400, Request ID: 48ab27e4-30db-4b0b-8d33-aa96499709c8)" (RequestToken: d1257c30-cdf4-abac-1bf3-240e031587a7, HandlerErrorCode: InvalidRequest)|
```

Need to create another subnet, make sure different AZ each, in this case we using the public ones so those need to be in diff AZ
![[Pasted image 20231102154104.png]]

New error
![[Pasted image 20231102180124.png]]
![[Pasted image 20231102180215.png]]
when picking the subnets pick to give public IPs


Issue:
When i  upload the code index.zip with index.php + images. Stops working
