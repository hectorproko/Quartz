**Step 1: Requirements**
- An AWS account.
- A Node.js application
  ![[nodejs-api-git-repo.zip]]
- AWS CLI installed 
- Docker installed 

![[Pasted image 20241207081200.png]]

**Step 2: Building and Testing the Web App**

> [!NOTE]- Review Dockerfile
> ```dockerfile
> # Use Node.js 14 as the base image
> FROM node:14
> 
> # Set the working directory inside the container
> WORKDIR /usr/src/app
> 
> # Copy package.json and package-lock.json files
> COPY package*.json ./
> 
> # Install dependencies
> RUN npm install
> 
> # Copy the entire application code into the container
> COPY . .
> 
> # Expose port 3000
> EXPOSE 3000
> 
> # Command to run the application
> CMD ["node", "app.js"]
> ```

> [!NOTE]- Review app.js file
> ```javascript
> const express = require('express');
> const app = express();
> 
> // Endpoint to return server status and uptime
> app.get('/status', (req, res) => {
>     res.json({
>         status: 'running test 8',
>         uptime: process.uptime(), // Uptime in seconds
>     });
> });
> 
> // Start the server on a specific port
> const PORT = 3000;
> app.listen(PORT, '0.0.0.0', () => {
>     console.log(`Server is running on port ${PORT}`);
> });
> ```
> 

Building an image and running it to test it:
 - Build and tag the Docker image: `docker build -t node-status-api .`
- Test the container locally: `docker run -p 3000:3000 node-status-api`

> [!done] Works
> ![[Pasted image 20241211090237.png]]

**Step 3: Configuring AWS CLI**
- Created an AWS CLI user `vyorius-demo` and attach the `AmazonEC2ContainerRegistryFullAccess` policy.

- Generate and configure AWS CLI credentials for this user.
  ![[Pasted image 20241207082545.png]]

**Step 4: Creating and Pushing the Docker Image to AWS ECR**

Created a private AWS ECR repository. 

Inside the repository I'll click "View push commands" to authenticate Docker with ECR, tag the image, and push it to the repository.


`aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 838427752759.dkr.ecr.us-east-1.amazonaws.com`

`docker build -t nodejs-api-repository .`

`docker tag nodejs-api-repository:latest 838427752759.dkr.ecr.us-east-1.amazonaws.com/nodejs-api-repository:latest`

`docker push 838427752759.dkr.ecr.us-east-1.amazonaws.com/nodejs-api-repository:latest`

