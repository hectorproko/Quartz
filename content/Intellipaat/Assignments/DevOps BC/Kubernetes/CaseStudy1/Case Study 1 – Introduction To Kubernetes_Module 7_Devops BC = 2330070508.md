
> [!info] Module 7: Case Study 1 - Introduction to Kubernetes
> **Problem Statement:** 
> You have just joined a startup Ventura Software as a DevOps Lead Engineer. The company relies on a monolithic architecture for its products. Recently, the senior management was hired. The new CTO insists on having a microservice architecture. The development team is working on breaking the monolith. Meanwhile, you have been asked to host a test application on Kubernetes to understand how it works. 
> 
> Following things have to be implemented: 
> 1. Deploy an Apache2 deployment of 2 replicas 
> 2. Sample code has been checked-in at the following GitHub repo: https://github.com/hshar/website.git You have to containerize this code, and push it to Docker Hub. Once done, deploy it on Kubernetes with 2 replicas. 
> 3. Deploy ingress with the following rules: 
>    a. */apache* should point to the Apache pods 
>    b. */custom* should point to the GitHub application