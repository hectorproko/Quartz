---
tags:
  - docker
---
> [!info] Docker Part 2 Assignment - 2
> **Tasks To Be Performed:** 
> 1. Use the Apache2 container created in previous module 
> 2. Create a bind mount on `/var/www/html` to replace html files dynamically 
> 
> Submit the commands to complete the assignment.

### Step 1: 
Using container `ID: cbda67fd188b` from [[Assignment 1 – Docker – II_Docker II_Devops BC = 2330070508|Assignment 1 – Docker – II]] 

%%I think i meesed up here, since it sounds like the container need to be running

I'll stop and remove previous container
![[Pasted image 20231116155033.png]]
%%

Removing container
```
docker rm -f cbda67fd188b
```

This command recreates a container with bind mounts, linking specific source and target paths from the local host to the container.
```bash
docker run -it --mount type=bind,source=/c/Users/Hecti/Desktop/docker_vol,target=/var/www/html -p 8080:80 -d hectorproko/my_docker_image:my_apache_image2
```
![[Pasted image 20231116160144.png]]

%%When you bind mount the destination gets replace with source so if source is empty destination gets deleted%%

### Step 2:
Created file `/index.html` inside folder nano `docker_vol`
`nano docker_vol/index.html`
```html
<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>Created in Bind Mount</h1>


</body>
</html>
```


Restarted the container
```bash
docker restart 0f3ceee8c91693
```

Verifying the the `index.html` is being hosted by accessing the container/Apache Server 

> [!success]
> ![[Pasted image 20231116160825.png]]