---
tags:
  - docker
---

> [!info] Docker Part 2 Assignment - 5
> **Tasks To Be Performed:** 
> 1. Use the previous assignment’s deployment 
> 2. Deploy any 2 containers in a overlay network 
> 3. Try pinging each of the containers from within the containers



### Step 1: Previous Deployment
Using previous [[Assignment 4 – Docker – II_Docker II_Devops BC = 2330070508|Assignment 4 – Docker – II]]'s Deployment

> [!info] Instances Private IPs
> master `10.0.1.199`
> worker1 `10.0.1.176`
> worker2 `10.0.1.38`


### Step 2: Deploy Two Containers in an Overlay Network

In this step, I will deploy two containers within an overlay network in the Docker Swarm cluster. An overlay network enables seamless communication between containers across different nodes in the Swarm. To achieve this, I will use the following commands:
```bash
# Create an overlay network (if not already created)
docker network create --driver overlay my-overlay-network

# Deploying two containers in the overlay network
docker service create --name container-1 --network my-overlay-network alpine ping 8.8.8.8
docker service create --name container-2 --network my-overlay-network alpine ping 8.8.8.8
```

![[Pasted image 20231117145641.png]]
%%seems like we need a program to run inside, why we running ping%%
%%  
> Yes, in a Docker Swarm cluster, it's common to create containers as services using the `docker service create` command rather than using `docker run`. When you create containers as services in a Swarm, they benefit from features like automatic load balancing, high availability, and easy scaling.

%%

### Step 3: Ping Containers from Within Containers

%%I first locate the Pods that are associated with the services named 'Container-1' and 'Container-2' using the following command:%%

I find out which node I need to ssh into
```bash
docker service ps <container-1>
```

![[Pasted image 20231117150323.png]]
![[Pasted image 20231117154014.png]]
So the containers are in worker1 `10.0.1.176` and worker2 `10.0.1.38`
%%
We see the node that the container is in

> [!attention]
> The reason the `docker ps` command doesn't show the container with the ID `3kpp0efxbkcg` is because it's a container managed by a Docker Swarm service, and `docker ps` typically only lists containers that are running directly on the Docker host where you run the command.

%%
%%
Once we have `ssh` into each node we run the following commands:

```bash
# Execute a shell inside container-1
docker exec -it container-1.1 sh

# Inside container-1, ping container-2 by its service name
ping container-2
```
%%

I SSH into worker1  and subsequently log into 'container-1,' enabling me to ping 'container-2'.

> [!success]
> ![[Pasted image 20231117153511.png]]

This time, I SSH into worker2, which allows me to log into 'container-2.' From within 'container-2,' I execute a ping command to reach 'container-1'.

> [!success]
> ![[Pasted image 20231117154220.png]]


