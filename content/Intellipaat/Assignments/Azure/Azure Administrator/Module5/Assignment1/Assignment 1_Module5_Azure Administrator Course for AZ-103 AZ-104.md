==Pending CleanUP==
---
tags:
  - azure
---
> [!info] Module 5: Assignment - 1
> **Tasks To Be Performed:** 
> 1. Install a Docker using VM 
> 2. Pull hshar/webapp (https://hub.docker.com/r/hshar/webapp) repository 
> 3. Create a new file in this repository


### Step 1: Install Docker on a Virtual Machine

1. **I Create a Linux VM**:
    
    - Will use the VM from [[Assignment 5_Module4_Azure Administrator Course for AZ-103 AZ-104|Assignment 5: Module 4]] 
      
      %%This is why it had Apache installed and cause you [[Assignment 1_Module5_Azure Administrator Course for AZ-103 AZ-104#^a0d827|issues]]%%
1. **I Install Docker Using `docker.io`**: ^f947ef
    - I run the following commands to update the package index and install Docker from the Ubuntu repositories:
      `sudo apt-get update`
      `sudo apt-get install docker.io`
    - After the installation, I start and enable Docker to ensure it's running and set to start on boot:
      `sudo systemctl start docker `
      `sudo systemctl enable docker`
    - I verify Installation
      `sudo docker --version`
      <br>![[Pasted image 20231207195403.png]]

### Step 2: Pull the `hshar/webapp` Docker Repository

1. **I Pull the Docker Image**:
    - I use the Docker command to pull the `hshar/webapp` image from Docker Hub:
      `sudo docker pull hshar/webapp`
      <br>![[Pasted image 20231207195804.png]]

### Step 3: Create a New File in the Repository

1. **I Run a Container from the Pulled Image**:
    
    - I start a Docker container using the `hshar/webapp` image:
      `sudo docker run -dit --name webapp-container hshar/webapp`
  
2. **I Access the Container's Shell**:
    
    - I access the shell of the running container:
      `sudo docker exec -it webapp-container bash`
  
3. **I Create a New File in the Container**:
    
    - Inside the container, I navigate to the desired directory.
    - I create a new file `touch newfile.txt`  

<br>![[Pasted image 20231210212045.png]]
### Step 4: Commit the Changes to Create a New Docker Image

1. **Commit the Container to a New Image**:
    
    - Use the `docker commit` command to create a new image from the container's current state.
    - The syntax is `docker commit [CONTAINER_ID] [new_image_name]:[tag]`.
2. **Verify the New Image**:
    
    - Use `docker images` to list all images and verify that your new image (`mynewimage:latest`) is there.

```bash
azureuser@VMCustomImage:~$ sudo docker commit f88acb1dcab07b1ae0 hshar/webapp_updated:latest
sha256:5d9250a92e2766f6b591a7ab647888a836ef9da9ea779a098abcce830ee2e284
azureuser@VMCustomImage:~$ sudo docker images
REPOSITORY             TAG       IMAGE ID       CREATED          SIZE
hshar/webapp_updated   latest    5d9250a92e27   8 seconds ago    303MB
<none>                 <none>    853e35c08c74   30 seconds ago   303MB
hshar/webapp           latest    0cbc1f535ed8   4 years ago      303MB
azureuser@VMCustomImage:~$
```

<br>![[Pasted image 20231210212722.png]]

%%
By completing these steps, you will have installed Docker on a Linux VM, pulled the `hshar/webapp` Docker repository, and created a new file within this repository. After creating the new file inside the running Docker container, you then commit these changes to create a new Docker image.
%%

%%

> [!question] Issue
> 
> > [!fail]
> > Addition test I did
> > run that image I created as container and access it using VM Public IP, made sure port 80 was opened
> > ```
> > sudo docker run -d -p 8080:80 --name mywebapp hectorregistry.azurecr.io/webapp_updated:latest
> > ```
> > Here we get appache deault page
> 
> but when using App Service we get
> <br>![[Pasted image 20231213123114.png]]
> 
> 
> > [!success]
> > The VM had apache running and the container was set to be access on port 8080, was using not only port 80 but also apache in the VM instead of container
> > <br>![[Pasted image 20231213150047.png]]
> 

%%

^a0d827
