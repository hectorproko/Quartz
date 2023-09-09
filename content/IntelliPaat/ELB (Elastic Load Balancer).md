# Intellipaat
## Lecture 1 – ELB Introduction

Load balancer is a service that uniformly distributes the network traffic and workloads across multiple servers or a cluster of servers. Load balancer increases the availability and fault tolerance of an application

- Elastic Load Balancer (ELB) is a load balancing service for the AWS deployments
- ELB scales itself as necessary to handle the load
- Incoming traffic is distributed across EC2 instances in multiple availability zones
- Load balancer is the single point of contact for clients

## Lecture 2 – Types Of Load Balancer

### Classic Load Balancer
<mark style="background: #FFB8EBA6;">Now deprecated by AWS</mark>
- Distributes the incoming application traffic across EC2 instances in multiple AZs and functions at [[osi_layer7_Application|Layer 7]] of the [[OSI Model (Open Systems Interconnection Model).canvas|OSI model]]
- Routes the traffic to healthy instances only, and it is evenly distributed
- Internet and Internal-facing load balancer

### Application Load Balancer
- Functions at the [[osi_layer7_Application|7th layer]] of the [[OSI Model (Open Systems Interconnection Model).canvas|OSI model]]
- Identifies the incoming resource type and directs it to the appropriate sewer
- Suitable for less demanding web architectures that don't require high performance.

### Network Load Balancer
- Functions at the [[osi_layer4_Transport|4th layer]] of the [[OSI Model (Open Systems Interconnection Model).canvas|OSI model]]
- Handles millions of requests per second and maintains low latency
- Ideal for load balancing the TCP traffic and supports elastic or static IP

### Gateway Load Balancer
Gateway Load Balancing automatically distributes your incoming traffic across multiple targets in one or more Availability Zones, such as EC2 instances, containers, and IP addresses. It monitors the health of its registered targets and routes traffic only to those that are in good condition.

**Benefits of Gateway Load Balancer**
- Easier deployment of third-party virtual appliances.
- Scalability based on demand.
- Increased availability and reliability.
- Provides endpoints for a more secure and reliable connection.

**Steps to Create Gateway Load Balancer**
- Because your clients can only communicate with the load balancer using IPv4 addresses, you must select IPv4 as the IP address type.
- Select the service provider VPC for VPC.
- Select all of the Availability Zones in which you launched security appliance instances, as well as the corresponding public subnets, for Mappings.
- Choose a target group to which traffic should be routed as the default action. Create a target group first if you don't already have one. The GENEVE protocol must be used by the target group.

## Demo 1 – Creating Application Load Balancer
#chat #miniProject 
> [!NOTE]- Steps: Creating Application Load Balancer
> Certainly! Here's a step-by-step guide to replicate the demo on creating an Application Load Balancer with instances running Apache and Nginx web servers.
> 
> ### Prerequisites
> - AWS Account
> - Basic knowledge of AWS EC2 and Load Balancers
> 
> ### Steps
> 
> #### Create EC2 Instances
> 1. **Navigate to EC2 Dashboard**: Log into your AWS Management Console and go to the EC2 dashboard.
> 2. **Launch Instance**: Click "Launch Instance" to create a new EC2 instance.
> 3. **Select AMI**: Choose the "Ubuntu" as your Amazon Machine Image (AMI).
> 4. **Configure Instance**: Select your desired configurations; for this demo, defaults are mostly fine.
> 5. **Security Groups**: Edit security groups to allow all incoming traffic.
> 6. **Launch Instance**: Click on "Launch Instance" and create two instances.
> 
> #### Rename Instances
> 1. **Rename to Apache2**: Rename one instance to "Apache2".
> 2. **Rename to Nginx**: Rename the other instance to "Nginx".
> 
> #### Create Target Group
> 1. **Navigate to Load Balancer Section**: While your instances are initializing, go to the "Load Balancers" section in EC2.
> 2. **Create Target Group**: Click on "Create Target Group".
> 3. **Target Group Settings**: Choose "Instances" as the target type. Name the target group and select the "HTTP" protocol.
> 4. **Associate Instances**: Add the two instances you created to this target group.
> 
> #### Create Load Balancer
> 1. **Navigate to Load Balancers**: Go back to the "Load Balancers" section.
> 2. **Create Load Balancer**: Choose "Application Load Balancer" and provide it a name.
> 3. **Configure Settings**: Choose "Internet-facing", select the VPC, and attach all subnets.
> 4. **Security Group**: Select the same security group as your instances.
> 5. **Target Group**: Attach the target group you created earlier.
> 6. **Create**: Click on "Create Load Balancer".
> 
> #### Update and Install Web Servers
> 
> 1. **SSH into Apache2**: SSH into the instance you named "Apache2".
> ```bash
> sudo apt-get update sudo apt-get install apache2
> ```  
>  
> 2. **SSH into Nginx**: SSH into the instance you named "Nginx".
> ```bash
> sudo apt-get update 
> sudo apt-get install nginx
> ```
> 
> #### Test Load Balancer
> 1. **Load Balancer DNS**: Go back to the "Load Balancers" section and copy the DNS name of your Load Balancer.
> 2. **Test**: Paste the DNS name into a web browser. Refreshing the page should alternate between the Apache and Nginx default pages, showing that load balancing is working.
> 
> And that's it! You've successfully set up an Application Load Balancer with Apache and Nginx instances.
## Demo 2 – Creating Network Load Balancer
#chat #miniProject 
> [!NOTE]- Steps: Creating Network Load Balancer
> Certainly! The presenter provides a walkthrough on how to set up a Network Load Balancer on AWS with two instances running Apache2 and Nginx. Below are the steps to replicate the demo:
> 
> ### Prerequisites
> - Two AWS EC2 instances running; one with Apache2 and another with Nginx.
> 
> ### Steps
> 1. **Navigate to AWS Network Load Balancer**: Open your AWS console and go to the Network Load Balancer section.
>     
> 2. **Create a Network Load Balancer**: Click on 'Create' and fill in the necessary details.
>     
>     - Load Balancer Name: Name it as you like (e.g., "network load balancer").
>     - Scheme: Choose 'Internet-facing'.
>     - IP address: Choose 'IP'.
>     - VPC: Choose the 'Default VPC' where your instances are running.
>     - Availability Zones: Select all availability zones for mapping.
>     - Port Configuration: Make sure it’s set to port 80.
> 3. **Create a Target Group**: In the same window, look for an option to create a target group.
>     
>     - New tab opens: Create a target group for Network Load Balancer.
>     - Target Type: Choose 'Instance'.
>     - Name: Give a name (e.g., "network load balancer target group").
>     - Protocol: Choose 'TCP'.
>     - Health Checks: Choose 'TCP'.
> 4. **Add Instances to Target Group**:
>     
>     - After creating the target group, you will see a list of running instances.
>     - Select the two instances (Apache2 and Nginx) you want to associate with the load balancer.
> 5. **Associate Target Group with Load Balancer**:
>     
>     - Select the target group that you just created.
> 6. **Create Load Balancer**: Click on the 'Create Load Balancer' button.
>     
> 7. **Wait for Health Checks and Activation**:
>     
>     - Once created, the load balancer will perform health checks and move to the 'Active' state.
> 8. **Test the Load Balancer**:
>     
>     - Once it's active, take the DNS name of the load balancer and paste it in your web browser.
>     - Refresh the page multiple times to see traffic routed between Apache2 and Nginx instances.
> 
> ### Note:
> 
> - Make sure you enable all traffic for the security group or at least allow TCP.
> - The presenter mentions that Network Load Balancer should be chosen over Application Load Balancer when you require ultra-high performance or expect high traffic.
> 
> And there you go! You should have a working AWS Network Load Balancer distributing traffic between two instances running Apache2 and Nginx.

## Lecture 3 – Architecture And Weighted Routing In Load Balancer

**Load Balancer Architecture:**
- A load balancer receives incoming web traffic and distributes it across multiple servers (instances), depending on their health status.
- Instances can be located in different availability zones.
- The load balancer continuously checks the health of instances and directs traffic only to healthy instances.

**Weighted Routing:**
- In the load balancer, you have an option for weighted routing.
- You can define which target group or instance should receive the majority of the traffic and which should not.
- For example, if 10 requests are coming to your website, you can specify that 70% should go to target group A, and 30% to target group B.
- This allows for effective traffic management and decision-making for managing a website.

**Cross-Zone Load Balancing:**
- By default, the load balancer distributes traffic only within the same availability zone. (when you create it you can choose which [[AZ (Availability Zone)_aws|AZ]] to include)
- Enabling cross-zone load balancing allows the distribution of incoming traffic across multiple zones.
- This ensures that no single instance or zone gets overloaded, balancing the load effectively.

**Connection Draining:**
- Sometimes an instance may fail health checks and need to be removed from the architecture.
- The process of safely removing this instance is known as connection draining.
- During this time, the architecture will not go down as other target groups will handle the incoming traffic.
- Once the instance is removed, you can investigate the issue, fix it, and then add it back to the architecture.


## Lecture 4 – Weighted Routing
#chat #miniProject 

> [!NOTE]- Steps: Weighted Routing
> Certainly! Below are the extracted steps based on your demonstration to set up weighted routing with AWS Application Load Balancer using Apache and Nginx web servers:
> 
> ### Preliminary Steps:
> 
> 1. **Setup Two Web Servers**: One with Apache and another with Nginx, both having public IPs.
> 
> ### Create Target Groups:
> 
> 1. **Go to AWS Console**: Navigate to EC2 and then Target Groups.
>     
> 2. **Create First Target Group**:
>     
>     - Name it 'target_group_1'.
>     - Choose 'Instance' as the target type.
>     - Choose the appropriate VPC.
>     - Click 'Next'.
>     - Register only the Nginx machine.
>     - Click 'Include as pending'.
>     - Click 'Create Target Group'.
> 3. **Create Second Target Group**:
>     
>     - Name it 'target_group_2'.
>     - Choose 'Instance' as the target type.
>     - Choose the appropriate VPC.
>     - Click 'Next'.
>     - Register only the Apache machine.
>     - Click 'Include as pending'.
>     - Click 'Create Target Group'.
> 
> ### Create Application Load Balancer:
> 
> 1. **Navigate to Load Balancers**: Create a new Load Balancer.
> 2. **Choose Type**: Select 'Application Load Balancer'.
> 3. **Configuration**:
>     - Name your load balancer.
>     - Choose the same VPC as your instances.
>     - Select all Availability Zones.
> 4. **Security Groups**: Attach the same security group(s) as your instances.
> 5. **Select Target Group**: Choose the first target group ('target_group_1').
> 6. **Create Load Balancer**: Confirm and create the Load Balancer.
> 
> ### Set Up Weighted Routing:
> 
> 1. **Navigate to Listeners**: Under your Load Balancer.
> 2. **Edit Listener**: Choose the listener and click 'Edit'.
> 3. **Attach Target Groups**: Attach both target groups.
> 4. **Set Weights**: Assign weights to both target groups (e.g., 8 for Nginx and 2 for Apache).
> 5. **Save Changes**: Confirm and save the settings.
> 
> ### Optional: Path-Based Routing
> 
> 1. **Connect to Apache Instance**: SSH into the Apache machine.
> 2. **Create a Directory and HTML file**: Make a directory called 'server1' and an 'index.html' inside it with some content.
> 3. **Go Back to Listener Rules**: Navigate back to the Listeners section in the AWS Console.
> 4. **Add Rule**: Click on 'View/Edit rules' and add a new rule.
>     - For path, specify `/server1/`.
>     - For action, choose to forward it to 'target_group_2'.
> 5. **Save Rule**: Confirm and save your rule.
> 
> ### Test Your Setup:
> 
> 1. **Copy Load Balancer DNS**: Go to the Load Balancer and copy its DNS name.
> 2. **Test in Browser**: Paste the DNS in a browser to see if the weighted and path-based routing are working.
> 
> And there you go! You should now have a working example of weighted routing between an Apache and an Nginx server, along with optional path-based routing.

## Lecture 5 – Sticky Session

- **Session Stickiness**: This refers to binding a user to a particular session so that if they get disconnected and come back, they are taken to the same state where they left off.
    
- **Advantages of Session Stickiness**:
    1. **User Experience**: A more seamless interaction for the user.
    2. **Data Transfer Efficiency**: No need to move user data between different instances.
    3. **Resource Utilization**: Better use of RAM and cache, as the user's session data is already stored on one machine.
- **How to Enable**: Session stickiness can be enabled in the "target group" settings of your load balancer.
    
- **Types of Session Stickiness**:
    1. **Duration-based**: The session stickiness lasts for a predefined period.
    2. **Application-Controlled**: The application manages the session lifecycle.
- **Cookies**: Managing session stickiness often involves the use of cookies.


## Demo 3 – Sticky Session

> [!NOTE]- Steps to Replicate the Sticky Session Demo:
> #### 1. Launch Instances
> 
> - Launch two instances on your preferred cloud platform.
> - On one instance, set up a default Apache web server.
> - On the other, set up a custom web server.
> 
> #### 2. Set Up Target Group
> 
> - Create a Target Group in your cloud dashboard.
> - Attach the two instances to this Target Group.
> 
> #### 3. Set Up Load Balancer
> 
> - Create a Load Balancer and associate it with the Target Group.
> 
> #### 4. Verify Functionality
> 
> - Use the Load Balancer's public DNS to access both web pages to make sure they are being routed correctly.
> 
> #### 5. Configure Sticky Sessions
> 
> - Go back to the Target Group settings.
> - Enable the Sticky Session feature and set the type (load balancer generated cookie or application cookie) and duration.
> 
> #### 6. Test Sticky Sessions
> 
> - After enabling sticky sessions, revisit the Load Balancer's public DNS.
> - Refresh the page to observe that you are now sticking to one instance, validating that the sticky sessions are working as expected.
> 
> #### 7. Inspect Cookies (Optional)
> 
> - You can further inspect cookies using browser developer tools to see how sessions are being managed.
> 
> And that should give you a functional demonstration of how sticky sessions work in a load-balanced environment.


![[Auto Scaling_aws#Lecture 8 – ELB And Auto Scaling Integration]]
