> [!NOTE]- 8 Live Session Continued
> ![[8 Live Session]]


![[Pasted image 20230811142831.png]]
So there are private portion of aws and public?

[[region_aws]]
[[AZ (Availability Zone)_aws]] minimum             need 3?

[[IP Address]]
- IPv4
- [[IPv6]]

### [[CIDR (Classes Inter-Domain Routing)]]
Ex: `192.168.0.0/24`
- when you see anything after / is a pool of IPs, multiple  IP are available and combined together
- a group of IPs
![[Pasted image 20230811154401.png|500]]
how to calculate the number of IPs inside in this case 256

![[Pasted image 20230811154650.png|500]]

Remember each 0 in the octet has a number you turn off/on
from right to left 1 - 128, you keep doubling the number

1 2 4 8 16 32 64 128
Which means /24 leave 8 bits ON, meaning all these are on adding all of them
to 255, which is the number of your last IP, not to be confused with 256 which is the number if IPs

Online tool CIDR: https://www.ipaddressguide.com/cidr

![[Pasted image 20230811162023.png]]


/32 means a single IP, not 0, so no pool of IPs cuse its only 1

### [[VPC (Virtual Private Cloud)_aws]]
