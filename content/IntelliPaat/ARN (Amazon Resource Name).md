

# Intellipaat

## Lecture 1 – IAM Introduction

Amazon Resource Names uniquely identify AWS resources. Every resource in AWS is provided with an ARN.

ARN Format:
```css
arn:partition:service:region:account-id:resource
arn:partition:service:region:account-id:resourcetype/resource
arn:partition:service:region:account-id:resourcetype:resource
```

Amason Resource name

EC2:
```css
Instance > am:aws:ec2:region:account-id:instance/instance-id
AMI > arn:aws:ec2:region::image/image-id
Key-pair > arn:aws:ec2:region:account-id:key-pair/key-pair-name
Network Interface > arn:aws:ec2:region:account-id:network-interface/eni-id
```

EBS:
```css
Volume > arn:aws:ec2:region:account-id:volume/volume-id
Snapshot > arn:aws:ec2:region:account-id:snapshot/snapshot-id
```

Other:
![[Pasted image 20230822115135.png]]