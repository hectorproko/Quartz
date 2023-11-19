> [!info] Module 8: Terraform Assignment - 4
> **Tasks To Be Performed:** 
> 1. Destroy the previous deployments 
> 2. Create a VPC with the required components using Terraform 
> 3. Deploy an EC2 instance inside the VPC

### Step 1
Destroying infrastructure from [[Assignment 3 – Terraform_Module 8_Devops BC = 2330070508|Assignment 3 – Terraform]]
![[Pasted image 20231115195447.png]]

### Step 2-3

```yaml
provider "aws" {
  region = "us-east-1"
}

resource "aws_vpc" "example_vpc" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "example-vpc"
  }
}

resource "aws_subnet" "example_subnet" {
  vpc_id            = aws_vpc.example_vpc.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-east-1a"

  tags = {
    Name = "example-subnet"
  }
}

resource "aws_internet_gateway" "example_igw" {
  vpc_id = aws_vpc.example_vpc.id

  tags = {
    Name = "example-igw"
  }
}

resource "aws_route_table" "example_rt" {
  vpc_id = aws_vpc.example_vpc.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.example_igw.id
  }

  tags = {
    Name = "example-route-table"
  }
}

resource "aws_route_table_association" "example_rta" {
  subnet_id      = aws_subnet.example_subnet.id
  route_table_id = aws_route_table.example_rt.id
}

resource "aws_security_group" "example_sg" {
  name        = "example-sg"
  description = "Example Security Group"
  vpc_id      = aws_vpc.example_vpc.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "example-security-group"
  }
}

resource "aws_instance" "example_instance" {
  ami           = "ami-0230bd60aa48260c6"
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.example_subnet.id
  associate_public_ip_address = true
  vpc_security_group_ids = [aws_security_group.example_sg.id]

  tags = {
    Name = "example-instance"
  }
}
```
In this configuration:

- A VPC is created with a specified CIDR block.
- A subnet is defined within the VPC.
- An Internet Gateway is attached to the VPC to allow communication with the internet.
- A route table with a default route to the Internet Gateway is created and associated with the subnet.
- A security group with basic rules for SSH access is defined and associated with the VPC.
- An EC2 instance is deployed within the created subnet and attached to the security group.

`terraform apply`
![[Pasted image 20231115205049.png]]

%%
> [!attention]- Issue: with `security_groups`
> 
> > [!fail]
> > ```bash
> > │ Error: creating EC2 Instance: InvalidParameterCombination: The parameter groupName cannot be used with the parameter subnet
> > │       status code: 400, request id: 3b2ef40d-a093-47af-a83f-b2d49d08a006
> > │
> > │   with aws_instance.example_instance,
> > │   on main.tf line 73, in resource "aws_instance" "example_instance":
> > │   73: resource "aws_instance" "example_instance" {
> > ```
> > ![[Pasted image 20231115203552.png]]
> > 
> 
> > [!done] Solution
> > When you're launching an EC2 instance in a VPC (as opposed to EC2-Classic), you need to specify a VPC security group using its ID, not its name.
> > 
> > Changed 
> > ```
> > security_groups = [aws_security_group.example_sg.name]
> > ```
> > to 
> > ```
> > vpc_security_group_ids = [aws_security_group.example_sg.id]
> > ```
> > 
> > 

%%

Just to test the instance i try to ssh into it
![[Pasted image 20231115211158.png]]
![[Pasted image 20231115210936.png]]''