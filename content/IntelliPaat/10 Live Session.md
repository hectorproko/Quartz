> [!attention]- Continuing 9 Live Session
>
> ![[9 Live Session]] 

[[VPC (Virtual Private Cloud)_aws]]
- He describes it as Software Defined Data Center [[SDDC]]
- VPC is nothing more than a collection of IP address. Because when you create a VCP you only get IP Address. A virtual boundary
- A virtual network inside AWS. Regional service

two types of vcps:
Default VPC - created in every Region. Always 172.31.0.0/16
Customer VPC

#chat
Yes, that's a concise way to put it! A [[subnet]], in the context of IP networking, is essentially a subdivision of a CIDR block. When you create a subnet, you're essentially carving out a smaller piece (a subset) of IP addresses from a larger CIDR block. This allows for more granular control and segmentation of network resources.

Mentioned [[IPAM]] when creating the VCP

- Mentioning benefits of subnetting. I think he covered broadcasting, how it reduces it. 
- Subnet is also a pool of IPs, technically (also a CIDR)
- Some IPs are reserved in a subnet
  - 10.0.0.0/16
  - First IP address is reserved for  the Network Address (10.0.0.0)
  - Second IP, 10.0.0.1, Reserved for the Router
  - Third 10.0.0.2 - DNS
  - 10.0.0.3 - Reserved for future use
  - last ip, 10.0.255.255, reserved for broadcast IP

![[Pasted image 20230811214501.png]]
AWS gives a restriction that your CIDR must be between /28 adn /16, make sure you have enough IPs for the reserved portion



Tier is a layer.

So if you have a server with web, db and app. Thats 1 tier

For multi tier, give a server to each component

Two Tier design mean 2 subnets (+2 for [[HA]] = 4)
in aws subnet can not expand AZs
![[Pasted image 20230811223928.png]]

Dev  Test Prod envrionment usually segreated By VCP. But now is popular to segreate by Account

Example:
requirements: 15 web, 10 app, 20 db

10%-20% exrace fro buffer just in case


![[Pasted image 20230813094817.png]]

He created 2 subnets in different AZs
10.0.0.64/26 <- we get this by addind 1 to the last ip of the one below
10.0.0.0/26 <- the last IP of this one is 10.0.0.63
then he asked why? These two represent the network address of the subnets

> [!NOTE] Find subsequent subnet
> Alright! Let's break this down.
> 
> You already have:
> 
> 1. 10.0.0.0/26
> 2. 10.0.0.64/26
> 
> <mark style="background: #FFF3A3A6;">Each /26 subnet has 64 IP addresses.</mark>
> 
> To find the subsequent subnets, you can continue adding 64 to the last octet of the starting address of the most recent subnet:
> 
> From 10.0.0.64/26, the next subnet will be: 10.0.0.128/26
> 
> And then: 10.0.0.192/26
> 
> You could continue this process, but after 10.0.0.192/26 the next block would spill over into 10.0.1.0 and so on.
> 
> Here's a generalized process for finding subsequent subnets:
> 
> 1. Determine the number of IP addresses in the subnet by calculating 2^(32−subnetmask).
> 2. Add that number to the last octet of the starting IP address of the most recent subnet. If the value exceeds 255, then carry over to the next octet.
> 3. The result is the starting address of the next subnet.
> 
> For your case: 
> Subnet mask: 26 
> Number of IP addresses: 2^(32−26) = 64
> 
> Keep adding 64 to the last octet to find the next subnets.