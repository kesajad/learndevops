# Docker and Docker Containers
## What is Docker?
Docker is an open-source platform where developers can containerize the application. Containers are accessible before Docker but have gained popularity as a result of Docker. The most crucial aspects of Docker are the Docker Engine and Docker Hub. The first one works on your local system to run your program, and the second one is similar to a cloud service where we can share our docker images with everyone.

## Before Docker and after docker
![image](https://github.com/kesajad/learndevops/assets/99335234/5647cefe-c157-4e29-91a9-6269da710c2f)

## What is Dockerfile?
The operating system (OS) libraries and dependencies required to run the application source code which is not reliant on the underlying operating system (OS) included in the Dockerfile, which is a standardized, executable component. Programmers may design, distribute, launch, run, upgrade, and manage containers using the open-source platform Docker. Enterprise Edition (EE) and Community Edition (CE) of Docker are both available. The Enterprise Version is for businesses and IT teams working on mission-critical production applications, while the Community Edition is suitable for small teams just learning Docker.
![image](https://github.com/kesajad/learndevops/assets/99335234/63d9837b-864e-45f9-bfa6-52dc803210dc)

## What is Dockerfile?
The Dockerfile uses DSL (Domain Specific Language) and contains instructions for generating a Docker image. Dockerfile will define the processes to quickly produce an image. While creating your application, you should create a Dockerfile in order since the Docker daemon runs all of the instructions from top to bottom.

## What is Docker Image?
An artifact with several layers and a lightweight, compact stand-alone executable package that contains all of the components required to run a piece of software, including the code, a runtime, libraries, environment variables, and configuration files is called a Docker image.

## What is Docker Container?
A container is a runtime instance of an image. Containers make development and deployment more efficient since they contain all the dependencies and parameters needed for the application it runs completely isolated from the host environment.

## Installation
https://docs.docker.com/engine/install/ubuntu/

## Dockerfile commands/Instructions
1. FROM
Represents the base image(OS), which is the command that is executed first before any other commands.

Syntax: 
FROM <ImageName>
Example: The base image will be ubuntu:19.04 Operating System.
FROM ubuntu:19.04

2. COPY
The copy command is used to copy the file/folders to the image while building the image. 

Syntax:
COPY <Source> <Destination>
Example: Copying the .war file to the Tomcat webapps directory
COPY target/java-web-app.war  /usr/local/tomcat/webapps/java-web-app.war

3. ADD
While creating the image, we can download files from distant HTTP/HTTPS destinations using the ADD command.
Syntax:
ADD <URL>
Example: Try to download Jenkins using ADD command 
ADD https://get.jenkins.io/war/2.397/jenkins.war

4. RUN
Scripts and commands are run with the RUN instruction. The execution of RUN commands or instructions will take place while you create an image on top of the prior layers (Image).
Syntax: 
RUN < Command + ARGS>
Example: 
RUN touch file

5. CMD
The main purpose of the CMD command is to start the process inside the container and it can be overridden.
Syntax:
CMD [command + args]
Example: Starting Jenkins 
CMD ["java","-jar", "Jenkins.war"]

6. ENTRYPOINT
A container that will function as an executable is configured by ENTRYPOINT. When you start the Docker container, a command or script called ENTRYPOINT is executed. It can’t be overridden.The only difference between CMD and ENTRYPOINT is CMD can be overridden and ENTRYPOINT can’t.

Syntax:
ENTRYPOINT [command + args]
Example: Executing the echo command.
ENTRYPOINT ["echo","Welcome to GFG"]

7. MAINTAINER
By using the MAINTAINER command we can identify the author/owner of the Dockerfile and we can set our own author/owner for the image.
Syntax: 
MAINTAINER <NAME>
Example: Setting the author for the image as a GFG author.
MAINTAINER  GFG author 

## Create a Dockerfile
- Create a file named Dockerfile.
- Add instructions in Dockerfile.
- Build Dockerfile to create an image.
- Run the image to create a container.

## Example 1: Steps To Create Dockerfile With Example(Jenkins)
In this example, we will write the Dockerfile for Jenkins and build an image by using Dockerfile which has been written for Jenkins and we will run it as a container.
### Step 1: Create a directory and create a file with the name Dockerfile.
### Step 2: Open the Dockerfile by using the vim editor and start writing the command that is required to build the Jenkins image.
Dockerfile for Jenkins image
We used JDK as a base image because Jenkins’s pre-requisite is JDK after that we added a command called MAINTAINER which indicates the author or owner of the docker file and we added the ENV variable where we set the path for the Jenkins and by using RUN command we are creating the path and by using ADD we are downloading the Jenkins and starting the .war file with the help of CMD command.
```
FROM openjdk:11-jdk
MAINTAINER Guruschools
LABEL env=production
ENV apparea /data/app
RUN mkdir -p $apparea
ADD https://get.jenkins.io/war/2.397/jenkins.war $apparea
WORKDIR $apparea
EXPOSE 8080
CMD ["java","-jar","jenkins.war"]
```
### Step 3: Build the image by using the below command with the help of Dockerfile and give the necessary tags. and the dot(.) represents the current directory which is a path for Dockerfile.
docker build -t jenkins:1 .
### Step 4: Run the container with the help image ID or tag of the image by using the below command.
docker run -d -p 8080:8080 <Imagetag/ID>
### Step 5: Accesses the application (Jenkins) from the internet with the help of host port and hostIP (HostIP: Port)
![image](https://github.com/kesajad/learndevops/assets/99335234/1d2c8c06-3b9c-4996-95b4-998457291a4f)
