# Depoly Web Application To AWS EC2 Instance In Private Subnet

![Figure 1: AWS ](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/image.png)

## Introducing the app we’ll work on 
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

![Figure 5: The pushed image on dockerhub ](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/dockerhub.PNG)

## Create the GitHub repo 
create the repo and upload the project files  

## Create config.yml 
This is a configuration file for a CI/CD pipeline using CircleCI. It includes two jobs: "test" for testing and "deploy" for deploying a Docker image to  Docker Hub and running it on an EC2 instance. 

## Deploying to AWS
## Create VPC 
![Figure 7: VPC](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/Screenshot%20(20).png)

## Create an internet gateway and attach it to the VPC 
![Figure 8: IGW](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/ig.png)


## Create a Public and Private Subnet in the VPC
Public Subnet:
To allow routing from/to into internet, Edit Route in Route Table, and Add an internet gateway 
![Figure 9: public Subnet](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/public%20sub.png)

then, configure Public Route table.
![Figure 10: Public RT](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/public%20rt.png)

Private Subnet:
![Figure 11: private Subnet](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/private%20sub.png)

then, configure Private Route table.
![Figure 12: Private RT](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/private%20rt.png)

## Create two security groups that allows HTTP (s) and SSH traffic. 
![Figure 13: SG](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/sg.png)

## Create two EC2 instances
- EC2 instance in public subnet:
![Figure 14: Public EC2](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/public-ec2.PNG)

- EC2 instance in private subnet:
![Figure 15: Private EC2](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/private-ec2.PNG)

## Create a NAT Gateway in Public Subnet
to enable connectivity to the internet in the private subnet
![Figure 16:](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/nat.png)

then, configure Private Route Table and add "nat gw" to the routes.

## Deploy the App to EC2 Instance using CircleCI
Read  [.circleci/config.yml](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/.circleci/config.yml)

after committing the config file, a pipeline is triggered in CircleCI
![Figure 17:](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/success.PNG)

this config file do ssh to private EC2 using the public EC2 to build the docker image, push to dockerhub and run the container.

## Test the app on the browser by IP Address 
In order to browse to the application using the Public IP of Public Subnet, use Reverse Proxy.
- install nginx then edit its configuration file.
- browse to the public ip to open the app.
- 
![Figure 18:](https://github.com/aseelmalkawi/dockerized-coffee-shop/blob/main/doc%20imgs/3.PNG)
