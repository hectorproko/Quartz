
> [!info] Docker Part 2 Assignment - 4
> **Tasks To Be Performed:**
> 1. Create a Docker swarm cluster with 3 nodes 
> 2. Deploy an Apache container with 4 replicas


### Step 1: Creating Security Group 

1. **Swarm Management Ports:**
    - TCP port 2377: This port facilitates communication between manager nodes and worker nodes. It's essential for all nodes in the Swarm cluster.
      
2. **Overlay Network Ports (if used):**
    - UDP and TCP ports 7946: These ports are utilized for control plane communication among nodes in the overlay network.
    - UDP port 4789: This port is employed for transporting overlay network data traffic. It's specifically used when using overlay networks with Docker services.
      
3. **Service Published Ports:**
    - In my Swarm setup, I have a web service running so I need to open the specific port configured for this service `80`.

![[dockerswarm security group.png]]
SSH access is set to allow connections from any source (`0.0.0.0`), for remote access to perform the activities I'm documenting. Additionally, to enhance security, all ports related to Docker are confined within the VPC CIDR range (`10.0.0.0/16`). Furthermore, HTTP connections are permitted from any source (`0.0.0.0`).

### Step 2: EC2 Instances

I will create three EC2 instances, each running Ubuntu 22.04, and configure them to use the specified security group. Additionally, I will enable public IP addresses for these instances to facilitate SSH access.

%%
> [!question]- Issue: EC2 not updating
> > [!fail]
> > Instance could not install anything
> 
> > [!done] Solution
> > There was no Outgoing rule present, so need to add on allowing the instance to initiate outside connections to 0.0.0.0
> 

[docker isntall docs](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
```bash
#!/bin/bash
# Add Docker's official GPG key:
sudo apt-get update -y
sudo apt-get install ca-certificates curl gnupg -y
sudo install -m 0755 -d /etc/apt/keyrings -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```
or

%%
Installing Docker in all instances:
```bash
#!/bin/bash
sudo apt-get update -y
sudo apt-get install docker.io -y
```

Documenting Docker version:
```bash
Docker version 24.0.5, build 24.0.5-0ubuntu1~22.04.1
```


> [!info] Instances Private IPs
> master `10.0.1.199`
> worker1 `10.0.1.176`
> worker2 `10.0.1.38`

%%
> [!question]- Issue: permission denied 
> 
> > [!fail]
> > ```
> > ubuntu@ip-10-0-1-199:~$ docker swarm init --advertise-addr=10.0.1.199
> > permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/swarm/init": dial unix /var/run/docker.sock: connect: permission denied
> > ```
> > 
> 
> > [!done] Solution
> > Either use `sudo` or add current user to the "docker" group `sudo usermod -aG docker $USER` to avoid using sudo
> 
> - Log out and log back in to apply the group changes.
> - After logging back in, you should be able to use Docker commands without `sudo`.

%%

On the **master** node, I initiate the Docker Swarm with the following command:
```bash
docker swarm init --advertise-addr=10.0.1.199
```
*This command initializes the Swarm and designates `10.0.1.199` as the advertised address, which is the address that other nodes in the Swarm will use to connect to the master node for management and coordination.*

![[Pasted image 20231117120103.png]]
*Additionally, it outputs a Docker Swarm join token, which is used by worker nodes to join the Swarm.*

%%Messed the IP above teh first time need to redo used`docker swarm leave --force`
%%



In worker1 and worker2, I use the token by running the `docker swarm join` command to join them to the cluster.
```bash
docker swarm join --token SWMTKN-1-57n206fb6tainmxdd8okzegjn70afvoyomi32o4dntg9bpqixo-761de69y7sbxrn1j2epll6ilf 10.0.1.199:2377
```
%%Had to used sudo, because i did n%%

I verify the nodes in the swarm by using the `docker node ls` command.
![[Pasted image 20231117120824.png]]



### Step 3: Deploying Apache Container with 4 Replicas
Now that I have set up a Docker Swarm cluster, I can deploy an Apache container with 4 replicas. On the master node, I will create a `docker-compose.yml` file with the following content:

```yaml
version: '3.8'

services:
  apache:
    image: httpd:latest
    deploy:
      replicas: 4
    ports:
      - "80:80"
```

I deploy the service:
```bash
docker stack deploy -c docker-compose.yml my-apache-stack
```

This configuration will create 4 replicas of the Apache container and distribute them across the Swarm nodes.
![[Pasted image 20231117121847.png]]


I check the container distribution:
```bash
docker service ps my-apache-stack_apache
```
![[Pasted image 20231117122941.png]]

To verify that the Apache page is up and running, I will use the public IP addresses of worker2 and the master node and access it through a web browser.

> [!success]
> ![[Pasted image 20231117123423.png]]
> ![[Pasted image 20231117123438.png]]
