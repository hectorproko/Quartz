
> [!NOTE] Module 3: Case Study - Containerization using Docker Part 1 
> **Problem Statement:** 
> You work as a DevOps Engineer in a leading software company. You have been asked to Dockerize the applications on the production server. The company uses custom software. Therefore, there is no pre-built container which can be used. 
> 
> Assume the following things: 
> 1. Assume the software to be installed is Apache 
> 2. Use an Ubuntu container 
> 
> The company wants the following things: 
> 1. Push a container to Docker Hub with the above config 
> 2. The developers will not be working with Docker, hence from their side you will just get the code. Write a Dockerfile which could put the code in the custom image that you have built.


[[Assignment 5 – Docker – I_Module 3_Devops BC = 2330070508|Assignment 5 – Docker – I]]
and then push to DockerHub?


![[Assignment 5 – Docker – I_Module 3_Devops BC = 2330070508#Steps]]

When the developer provides the code, which will likely consist of multiple files, I can update the Dockerfile to incorporate this new code. Then, I'll rebuild the image.
```Dockerfile
# Copy developer code into the appropriate directory in the container 
COPY website/ /var/www/html/
```

Similarly to what I did in [[Assignment 3 – Docker – I_Module 3_Devops BC = 2330070508|Assignment 3 – Docker – I]], I'll then upload the rebuilt image to DockerHub.
![[Pasted image 20231031195354.png]]
%%
```
C:\Users\Hecti>docker images
REPOSITORY         TAG       IMAGE ID       CREATED       SIZE
my_apache_image2   latest    79f2dbe4e0f0   6 hours ago   231MB
ubuntu             latest    e4c58958181a   3 weeks ago   77.8MB

C:\Users\Hecti>docker login
Authenticating with existing credentials...
Login Succeeded

Logging in with your password grants your terminal complete access to your account.
For better security, log in with a limited-privilege personal access token. Learn more at https://docs.docker.com/go/access-tokens/
```

%%

I tag the image with my Docker Hub username and desired repository name (I'll use ```my_docker_image``` as an example):
```
docker tag my_apache_image2:latest hectorproko/my_docker_image:my_apache_image2
```

Now, I push the tagged image to Docker Hub:
```
docker push hectorproko/my_docker_image:my_apache_image2
```
![[Pasted image 20231031194208.png]]

![[my_apache_image2 in dockerhub.png]]