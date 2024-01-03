---
tags:
  - docker
---
> [!info] Docker Part 2 Assignment - 1
> **Tasks To Be Performed:** 
> 1. Launch the Apache2 container created in previous module 
> 2. Create a Docker volume on /var/www/html 
>  
> Please submit the commands in order to complete this assignment. 


### Step 1:
I will use the Apache2 container that we pushed to DockerHub in [[Case Study 1 – Containerization Using Docker – Part 1_Module 3_Devops BC = 2330070508|Case Study 1 – Containerization Using Docker – Part 1]]
![[my_apache_image2 in dockerhub.png|500]]

### Step 2:
%%Referecing [[Devops BC = 2330070508#Lecture 1 – Docker Storage|Lecture 1 – Docker Storage]]
%%


First, I create a volume: `volume-sample`
```bash
docker volume create volume-sample
```

Then, I verify its creation by running:
```
docker volume ls
```

![[Pasted image 20231116130344.png]]

Now, I run a container from the image that was [[my_apache_image2 in dockerhub.png|pushed]] to DockerHub in [[Case Study 1 – Containerization Using Docker – Part 1_Module 3_Devops BC = 2330070508|Case Study 1 – Containerization Using Docker – Part 1]], and I attach the newly created Docker volume named `volume-sample`.

%%

> [!question]- **Issue:** `invalid mount`
> > [!fail]
> > ```bash
> > $ docker run -it --mount source="demo-vol",destination="/var/www/html" -d hectorproko/my_docker_image:my_apache_image2
> > docker: Error response from daemon: invalid mount config for type "volume": invalid mount path: 'C:/Program Files/Git/var/www/html' mount path must be absolute.
> > See 'docker run --help'.
> > ```
> > 
> 
> > [!done] Solution
> > The error you're encountering, `invalid mount path: 'C:/Program Files/Git/var/www/html'`, suggests that Docker is interpreting the mount path in a Windows-specific context, likely because you're running the command in a Git Bash or similar shell on Windows.
> > 
> > In Git Bash, paths starting with `/` are automatically translated to Windows paths, which leads to this confusion. To prevent this translation and use the Unix-style absolute path as intended, you can prefix the path with an extra `/`, like this:
> > ```bash
> > docker run -it --mount source="demo-vol",destination="//var/www/html" -p 8080:80 -d hectorproko/my_docker_image:my_apache_image2
> > ```
> > 
> 

%%

I run a Docker container and attached the newly created volume to it
```bash
docker run -it --mount source="volume-sample",destination="/var/www/html" -p 8080:80 -d hectorproko/my_docker_image:my_apache_image2
```


<!--
Big messup here, see like you attached a wrong volume, that i dont think even existed in your environemnt it was from the lesson
![[Pasted image 20231116155033.png]]
-->
I verify the container works by `curl`ing the page from localhost
![[Pasted image 20231116155018.png]]



