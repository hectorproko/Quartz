
# Intellipaat

## Lecture 6 – Auto Scaling Introduction

### 1. What is Auto Scaling?

Auto scaling is the process by which the number of instances in a system can be automatically adjusted based on the load on those instances. Here, "instances" can refer to servers, containers, or other compute resources. Auto scaling is particularly useful because it can dynamically allocate resources depending on real-time needs.

- **Load Parameters**: Auto scaling decisions can be made based on various metrics such as CPU utilization, network usage, etc.
- **Automation**: Auto scaling groups enable the automation of resource allocation, reducing the need for manual intervention.
- **Predictive Scaling**: Advanced auto scaling solutions can even predict future needs based on historical data and adjust resources proactively.

### 2. [[Vertical Scaling|Vertical]] and [[Horizontal Scaling|Horizontal]] Scaling
As far as I know AWS does only Horizontal

### 3. Lifecycle of Auto Scaling
![[Pasted image 20230829144747.png]]
The lifecycle of auto scaling involves several states that an instance might go through:

1. **Pending State**: The instance is being launched but is not yet in service.
2. **In-Service State**: The instance is now actively servicing requests.
3. **Health Checks**: A routine health check is performed. If the check fails, the instance moves to a "Terminating" state.
4. **Terminating State**: The instance is shutting down.
5. **Standby State**: If the instance is not needed, it can be moved to a standby state for future use.
6. **Detached State**: An instance can be detached from the auto scaling group and reused later.


## Lecture 7 – Components Of Auto Scaling

#### Auto-Scaling Components

**1. Groups**
- In an auto-scaling group, you specify the EC2 instances you want to use.
- The group settings include the maximum, minimum, and desired number of instances.
- Upon creation, the group will launch the desired number of instances.
- Additional instances will be launched or terminated based on policies you define.

**2. Configuration Templates**
- Think of a configuration template as the blueprint for your instances.
- It contains crucial details such as AMI, instance type, security groups, and more.
- Note: Once a launch configuration is created, it cannot be modified.

**3. Scaling Options**
- You have a choice to scale manually, dynamically, or based on a schedule.
- Scaling could also be driven by demand, reacting to metrics like CPU utilization or network throughput.

---
#### Scaling Policies
- These policies trigger based on CloudWatch alarms.
- You can set conditions like "If CPU utilization is above 70% for 5 minutes, then scale up."
- Minimum, maximum, and desired instance counts are also set here.

**Types of Scaling**
1. **Simple Scaling**: Waits for a "cool-down" period before acting on another trigger.
2. **Step Scaling**: Allows for more dynamic scaling without waiting for cool-down periods.

---
#### Instance Termination
- Instances are selected for termination based on multiple factors.
- Priority is given to instances in the Availability Zone with the most instances and the oldest launch configurations.
- Other factors like billing cycles may also be considered.

---
#### Pricing
- No additional fees for auto-scaling. You only pay for the instances you launch.


## Demo 4 – Auto Scaling Creation
#chat #miniProject 

> [!NOTE]
> Certainly! Creating an auto-scaling group in AWS involves a series of steps. Below, I've outlined those steps into a more structured and simplified format for you to easily follow:
> 
> ### Prerequisites:
> 
> - An AWS account
> - A running EC2 instance (for creating an AMI)
> 
> ### Steps:
> 
> #### Step 1: Understand Launch Configuration
> 
> - **Explanation**: A launch configuration is a template that an Auto Scaling group uses to launch EC2 instances. It contains information like AMI ID, instance type, key pairs, and security groups.
> 
> #### Step 2: Create an AMI (Amazon Machine Image)
> 
> 1. **Navigate to EC2 Dashboard**: Go to your AWS Console and click on EC2.
> 2. **Select the Instance**: Choose the running instance for which you want to create an AMI.
> 3. **Create Image**: Click on `Actions -> Image and templates -> Create image`.
> 4. **Specify Details**: Give your image a name and an optional description.
> 5. **Create**: Click on the `Create image` button.
> 
> - **Explanation**: You're creating an AMI based on an existing instance to use in your launch configuration.
> 
> #### Step 3: Create Launch Configuration
> 
> 1. **Navigate to Launch Configuration**: From EC2 Dashboard, go to `Launch Configurations`.
> 2. **Create**: Click on `Create launch configuration`.
> 3. **Details**:
>     - **Name**: Enter a name for the launch configuration.
>     - **AMI**: Choose the AMI you created.
>     - **Instance Type**: Choose an instance type like `t2.micro`.
>     - **Security Groups**: Choose the desired security group.
>     - **Key Pair**: Choose an existing key pair.
> 4. **Create**: Click `Create launch configuration`.
> 
> - **Explanation**: You specify all the details that the Auto Scaling group would need to launch an instance.
> 
> #### Step 4: Create Auto Scaling Group
> 
> 1. **Navigate**: Go back to the EC2 Dashboard and click on `Auto Scaling groups`.
> 2. **Create**: Click on `Create Auto Scaling group`.
> 3. **Specify Details**:
>     - **Name**: Give it a name.
>     - **Launch Configuration**: Choose the launch configuration you created.
>     - **Subnets**: Choose the available subnets where you want instances to be launched.
>     - **Health Checks**: Specify health check settings.
>     - **Group size**: Set `Minimum`, `Desired`, and `Maximum` number of instances.
> 4. **Create**: Click on `Create Auto Scaling group`.
> 
> - **Explanation**: The Auto Scaling group will ensure that the number of instances in your group scales up or down based on load or other criteria.
> 
> #### Step 5: Verify Auto Scaling Group
> 
> - **Navigate**: Go back to EC2 Dashboard to confirm that new instances have been created based on your Auto Scaling Group settings.
> - **Explanation**: It's important to check that your Auto Scaling group is functioning as expected.
> 
> #### Step 6: Delete Auto Scaling Group (Optional)
> 
> - If you no longer need the Auto Scaling group, navigate to `Auto Scaling groups`, select your group, and delete it to stop new instances from launching.
> - **Explanation**: Deleting the Auto Scaling group will stop it from launching or managing further instances.
> 
> Now you should have a fully functional Auto Scaling group based on the Launch Configuration you created.



## Lecture 8 – ELB And Auto Scaling Integration

### How ELB and Auto Scaling Group Interact

**Forward Information for Scaling**
ELB can inform the Auto Scaling Group about the incoming traffic. If more traffic is coming in, the Auto Scaling Group can prepare to scale out more instances if needed.

**Prior Knowledge**
Having this information in advance helps the Auto Scaling Group act more smoothly when it finally decides to scale in or out. The actual scaling happens based on triggers and scaling policies, but having prior knowledge makes the process quicker.

**Handling Low Traffic**
Similarly, if the incoming traffic is low, ELB can inform the Auto Scaling Group that it doesn't need to launch any more instances.

**Load Balancer and Instance Registration**
The Load Balancer automatically registers instances that are part of the Auto Scaling group. This means that when new instances are launched due to scaling policies, they are automatically added to the Load Balancer's list of targets for traffic distribution.

### Health Checks: Two Types Explained

**EC2 Instance-Only Checks**
In this configuration, the health of an EC2 instance is evaluated solely based on EC2 status checks. If the EC2 instance passes these checks, it is considered healthy and traffic will be forwarded to it by the Load Balancer.

**EC2 and ELB Health Checks**
In a more comprehensive setup, an instance's health is determined by both EC2 status checks and Elastic Load Balancer (ELB) health checks. An instance is considered unhealthy if it fails either of these checks. In such a case, the Load Balancer will cease to forward traffic to the unhealthy instance until it passes the health checks again.

This dual-layer health check provides a more robust system for evaluating the health of instances. It ensures that traffic is only forwarded to instances that are both operational and able to handle the traffic efficiently.