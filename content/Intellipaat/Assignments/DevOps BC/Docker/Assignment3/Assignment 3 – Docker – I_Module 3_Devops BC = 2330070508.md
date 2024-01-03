---
tags:
  - docker
---

> [!info] Module 3: Docker Part 1 Assignment - 3
> **Tasks To Be Performed:** 
> 1. Use the saved image in the [[Assignment 2 – Docker – I_Module 3_Devops BC = 2330070508|previous assignment]] 
> 2. Upload this image on Docker Hub 
> 3. On a separate machine pull this Docker Hub image and launch it on port 80 
> 4. Start the Apache2 service 
> 5. Verify if you are able to see the Apache2 service

**I use the saved image from the previous assignment.**

First, I ensure that the image ```ubuntu_apache``` is present:
```
docker images
```
![[Pasted image 20231031000424.png]]

---

**I upload this image to Docker Hub.**

Before uploading, I need to log in to Docker Hub:
```
docker login
```
![[Pasted image 20231031100200.png]]
*I had a [DockerHub](https://hub.docker.com/) account already*

Then, I tag the image with my Docker Hub username and desired repository name (I'll use ```my_docker_image``` as an example):
```
docker tag ubuntu_apache:latest hectorproko/my_docker_image:latest
```
![[Pasted image 20231031101414.png]]

![[Pasted image 20231031100952.png|400]]
*Created repo before upload*

Now, I push the tagged image to Docker Hub:
```
docker push hectorproko/my_docker_image:latest
```
![[Pasted image 20231031102311.png|420]]

---

**On a separate machine, I pull this Docker Hub image and launch it on port 80.**

First, I pull the image:
```
docker pull hectorproko/my_docker_image:latest
```
![[Pasted image 20231031104337.png]]

Then, I run the container, mapping port 80:
```
docker run -it -p 80:80 hectorproko/my_docker_image:latest
```

---

**I start the Apache2 service.**

Inside the container's shell:
```
service apache2 start
```

---

**I verify if I can access the Apache2 service.**

I open my web browser and navigate to ```http://localhost```. I should see the Apache2 Ubuntu default page.
![[Pasted image 20231031104820.png|400]]

---
