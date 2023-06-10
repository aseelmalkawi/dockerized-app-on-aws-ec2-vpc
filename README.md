# Depoly Web Application To AWS EC2 Instance In Private Subnet

![Figure 1: AWS ](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/Project.drawio.png)

## Introduce the app we’ll work on 
We have a coffee shop application we chose to work on to deploy to AWS using CircleCi as a CICD tool. We’ll containerize the application and pull the image from the EC2 that we’ll create. 
In the below image, the application is opened locally still before we start the whole process. 

![Figure 2: coffee shop website locally](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/msedge_1inVKD2FgN.jpg)

## Create a docker file and test the image 
This Dockerfile is used to create a Docker image based on the nginx:stable image. It sets up a basic Nginx server to serve static web content. 

![Figure 3: The Dockerfile ](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/dockerfile.png)

To build the Docker image using the Docker file, you can use the docker build command. 

![Figure 4: Building the docker image ](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/powershell_WIOzNVz4vb.png)

After we built the Dockerfile and run it, we could access the application locally through localhost:80. 

## Push the image to the docker hub 
After finishing the Dockerfile and building the image, we finally tagged it and pushed it to dockerhub, so the EC2 can pull it later through CircleCi. 

![Figure 5: The pushed image on dockerhub ]()

## Create the GitHub repo 
We create the repo and upload the project files  

## Create config.yml 
This is a configuration file for a CI/CD pipeline using CircleCI. It includes two jobs: "test" for testing and "deploy" for deploying a Docker image to  Docker Hub and running it on an EC2 instance. 

## Create VPC 
![Figure 7:](image link)

## Create a Public Subnet in the VPC
To allow routing from/to into the rnnetEdit Route in Route Table, and Add an internet gateway 
![Figure 8:](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/public%20sub.png)

## Create an internet gateway and attach it to the VPC 
![Figure 9:](image link)

## Create a security group that allows HTTP (s) and SSH traffic. 
![Figure 10:](image link)

## Create an EC2 instance in the public subnet 
![Figure 11:](image link)

## Deploy the App to EC2 Instance 
![Figure 12:](image link)

## Test the app on the browser by IP Address 
![Figure 13:](image link)
