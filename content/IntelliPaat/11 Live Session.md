[[Internet Gateway]] allows you to communicate with the outside your VPC

[[subnet]] needs to be attached to a [[route table]]
a subnet is private until you make it aware of the internet gateway. In it route table there is an entry to the internet gateway

each subnet get a route table created when you create it?

You can attach only one internet gateway to 1 VPC

vpc peering, is like a private

**VPC Level**: When you create a VPC, it spans all the AZs in that region. Within that VPC, you can create subnets. These subnets can be associated with a specific AZ.

![[Pasted image 20230814130756.png]]

You need to mention in your route tablet the peering connection

There is a service quota section where you can adjust some limits like, number of connection of VCP