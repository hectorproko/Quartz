
# Intellipaat

## Lecture 6 – Introduction To CloudWatch

### Introduction

- **Topic**: Introduction to CloudWatch
- **Key Takeaway**: CloudWatch is a monitoring service by AWS that helps you track various metrics and events.

---

### Core Features of CloudWatch

1. **Alarms**: Create and set alarms based on specific conditions.
2. **Notifications**: Get notified about specific events.
3. **Dashboards**: Customize and create dashboards to monitor various metrics.
4. **Billing Alarms**: Track your AWS service costs and set up alarms for billing.

**Example**:

- You can set up an alarm to notify you when your AWS account bill goes over $100.

---

### Key Terminologies

1. **Dimension**: A name-value pair that helps identify a metric.
    
    - **Example**: For EC2 instances, the instance ID can be used as a dimension to find specific metrics.
2. **Statistics**: Data over a period of time that helps in analysis.
    
    - **Example**: For EC2 instances, this could be how long the instance has been running.
3. **Namespace**: A container for CloudWatch metrics.
    
    - **Note**: You need to specify a namespace for each data point you publish in CloudWatch.
4. **Metric**: Conditions you specify to monitor.
    
    - **Example**: CPU utilization for an EC2 instance can be a metric.

---

### How Metrics Work in AWS Services

- AWS services send metrics to CloudWatch by default.
- You can customize these metrics as per your needs.

---

### Specific Metrics for Different AWS Services

1. **EC2**
    
    - CPU Utilization
    - Disk Utilization
    - Network Interface interactions
    - CPU Credit Metrics
2. **EBS**
    
    - Read/Write Operations
    - Disk Utilization
3. **S3**
    
    - Number of Bad Requests
    - Upload/Download Metrics
    - Storage Metrics
4. **DynamoDB**
    
    - Query Metrics
    - Read/Write Operations
5. **Auto Scaling Groups**
    
    - CPU Utilization
    - Min/Max Group Size
    - Pending States

---

### Monitoring Architecture

- Metrics are collected from various AWS services.
- These metrics can be viewed either directly in the CloudWatch console or via email notifications.


  
## Lecture 7 – CloudWatch Dashboard And IAM

### CloudWatch Dashboard

The CloudWatch dashboard provides an interactive visual representation of the data associated with your AWS services and resources. Here are some points:

- **Widgets**: You can add different types of widgets like graphs (line graphs, stacked area graphs, etc.) and numbers.
- **Alarms**: You can display alarms you have set up to monitor for specific conditions like cost overruns or CPU utilization spikes.
- **Customization**: You can customize the time period for the metrics displayed and can view data in real-time or historical formats.

### CloudWatch Alarms

CloudWatch alarms are set up to notify you when certain thresholds are reached. These can be related to:

- **CPU Utilization**: An alarm can be set if the CPU usage goes above or below a certain percentage.
- **Cost**: You can set an alarm if your AWS cost goes above a certain dollar amount.
- **Network Metrics**: For example, incoming/outgoing network packets.

### Alarm States

Alarms have different states:

1. **OK**: The metric is within the defined threshold.
2. **Alarm**: The metric is outside of the defined threshold.
3. **Insufficient Data**: The metric data is not available or insufficient to determine the state.

### Notifications

You can integrate CloudWatch with [[SNS (Simple Notification Service)]] to receive notifications through various channels like email, SMS, or even triggering AWS Lambda functions when an alarm state changes.

### Logs and Events

Beyond metrics and alarms, CloudWatch also enables you to collect logs and events, which can further help in debugging or understanding the behavior of your services and applications.

By pulling all of this information into a centralized dashboard, CloudWatch allows you to have a unified view of the health and performance of your AWS resources and applications. This is invaluable for maintaining operational excellence, performing root cause analysis when issues arise, and even for cost-management purposes.


## Demo 4 – Creating CloudWatch Dashboard
#miniProject 
Not even going to put the steps basic and wrong
I guess lets wait until we do assigments

## Demo 5 – Creating CloudWatch Alarm

## Demo 6 – Creating Billing Alarm
Same thing

