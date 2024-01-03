> [!info] Docker Part 2 Assignment - 3
> **Tasks To Be Performed:**
> 1. Create 5 custom container with 5 different default pages 
> 2. Using Docker Compose deploy these 5 containers on port 81, 82, 83, 84 and 85 respectively

### Step 1: 

I will create five directories, each containing a custom 'index.html' file. These directories will serve as the bind mounts for individual containers. I will use the same `docker_vol` directory as in [[Assignment 2 – Docker – II_Docker II_Devops BC = 2330070508|Assignment 2 – Docker – II]].

![[Pasted image 20231116164203.png]]

Crafting docker compose file `docker-compose.yml`
```yaml
version: '3'

services:
  container1:
    image: httpd
    ports:
      - "81:80"
    volumes:
      - /c/Users/Hecti/Desktop/docker_vol/container1:/var/www/html

  container2:
    image: httpd
    ports:
      - "82:80"
    volumes:
      - /c/Users/Hecti/Desktop/docker_vol/container2:/var/www/html

  container3:
    image: httpd
    ports:
      - "83:80"
    volumes:
      - /c/Users/Hecti/Desktop/docker_vol/container3:/var/www/html

  container4:
    image: httpd
    ports:
      - "84:80"
    volumes:
      - /c/Users/Hecti/Desktop/docker_vol/container4:/var/www/html

  container5:
    image: httpd
    ports:
      - "85:80"
    volumes:
      - /c/Users/Hecti/Desktop/docker_vol/container5:/var/www/html
```



I execute the Docker Compose file using the `docker-compose up -d` command.
![[Pasted image 20231116165500.png]]

I test one of the ports to access the custom page hosted by one of the containers.

> [!success]
> ![[Pasted image 20231117101002.png]]

%%Testing the rest
![[5containers.gif]]%%