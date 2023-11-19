---
tags:
  - AWS
---
==Pending CleanUP==
 
1. **Target Tracking Scaling**: This is the policy you mentioned. It adjusts the number of EC2 instances in your group to maintain a specified metric value, such as average CPU utilization, close to the target value you set.
   ==Used in [[Case Study – ELB, ASG And Route 53_Module4_AWS Weekday BC = 2301080808#^b2587c|Case Study – ELB, ASG And Route 53]]==
    
2. **Step Scaling**: This policy increases or decreases the current capacity of the group based on a set of scaling adjustments, depending on the size of the alarm breach.
    
3. **Simple Scaling**: With this policy, EC2 Auto Scaling adjusts the desired capacity of your group based on a single scaling adjustment.
    
4. **Scheduled Scaling**: Instead of responding to changes in conditions, this strategy lets you increase or decrease the desired capacity of your Auto Scaling group based on known usage patterns. For instance, you can set it to scale up every morning when usage increases and scale down every night when usage decreases.
    
5. **Predictive Scaling**: Exclusive to AWS Auto Scaling and combines the best of proactive and reactive scaling. This policy predicts future traffic, including daily and weekly patterns, and schedules the right number of EC2 instances in advance of anticipated changes.