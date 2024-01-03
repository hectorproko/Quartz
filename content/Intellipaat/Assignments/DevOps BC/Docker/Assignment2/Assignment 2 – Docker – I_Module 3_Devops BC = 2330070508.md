---
tags:
  - docker
---

> [!info] Module 3: Docker Part 1 Assignment - 2
> **Tasks To Be Performed:** 
> 1. Save the image created in [[Assignment 1 – Docker – I_Module 3_Devops BC = 2330070508|assignment 1]] as a Docker image 
> 2. Launch container from this new image and map the port to 81 
> 3. Go inside the container and start the Apache2 service 
> 4. Check if you are able to access it on the browser



**To save the image created in [[Assignment 1 – Docker – I_Module 3_Devops BC = 2330070508|assignment 1]] as a Docker image.**

First, I'll find the container ID of the container I used:
```
docker ps -a
```
<br>![[Pasted image 20231031000228.png]]

With the container ID in hand, I commit it as an image. Let's name it `ubuntu_apache`:
```
docker commit eb2219bab5ad ubuntu_apache
```
<br>![[Pasted image 20231031000424.png]]
*Confirming image was created*

---

**I launch a container from this new `ubuntu_apache` image and map the port to 81.**

```
docker run -it -p 81:80 ubuntu_apache
```

==Once executed, I am inside the container's shell.==

> Even though I'm already in the container's shell, if I ever exit and need to return, I can use:
> ```
> docker exec -it [container-id] /bin/bash
> ```

---

Then, I start the Apache2 service:
```
service apache2 start
```

---

**I open my web browser to access the Apache2 page.**

By navigating to `http://localhost:81`, I should see the Apache2 Ubuntu default page.

> [!success]
> <br>![[Pasted image 20231031000835.png]]