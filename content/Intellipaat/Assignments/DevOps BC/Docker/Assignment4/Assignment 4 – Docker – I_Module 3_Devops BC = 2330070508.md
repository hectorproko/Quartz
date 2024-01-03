---
tags:
  - docker
---

> [!info] Module 3: Docker Part 1 Assignment - 4
> **Tasks To Be Performed:** 
> 1. Create a Dockerfile with the following specs:
>   - Ubuntu container
>   - Apache2 installed
>   - Apache2 should automatically run once the container starts 
> 2. Submit the Dockerfile for assignment completion

**Dockerfile:**
```Dockerfile
# Using the Ubuntu base image
FROM ubuntu:latest

# Updating the package list and installing Apache2
RUN apt-get update && apt-get -y install apache2

# Exposing port 80 for Apache2
EXPOSE 80

# Command to run Apache2 in the foreground
CMD ["apachectl", "-D", "FOREGROUND"]
```

1. I chose to use the `ubuntu:latest` tag to ensure I'm using the latest version of the Ubuntu image.
2. I combined the `RUN` commands into one line to make the image more efficient by reducing the number of layers.
3. I decided to go with `CMD` instead of `ENTRYPOINT` for starting Apache. This gives me the flexibility to override the command if needed when running the container in the future.