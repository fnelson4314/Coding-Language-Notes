## Docker

## What is Docker

- Docker is a tool for running applications in an isolated environment, similar to a virtual machine
- Docker uses containers which are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in user spaces.

## Images

- An image is a template for creating an environment of your choice
- You can also keep snapshots/versions of your images so in case you find an error in one, you can simply go back to a different version whenever
- Has everything you need to run your apps
- You can create your own images or you can find them publicly online at **hub.docker.com** where you can then do **docker pull [image]**
- To see a list of all your current images, you can run **docker images**
- You can remove an image using **docker image rm [imageId]**

## Containers

- A container is simply a running instance of an image
- To run a container from an image, you can run **docker run --name [containerName] -d -p [hostPort]:[containerPort] [image]:[tag]**
  - The -d flag tells the container to run in detached mode
  - The -p flag allows you to specify a port to connect the local host to the container port
- To stop a container, you can do it directly from the docker app or on the command line with **docker stop [containerId/containerName]**
- You can start an already existing stopped container by doing **docker start [containerName]**
- To remove a container, you can do it from the docker app or run **docker rm [containerId/containerName]**
  - To remove all containers, run **docker rm -f $(docker ps -aq)**
- To see the list of all containers (running and stopped), run **docker ps -a**

## Dockerfiles

- Dockerfiles are where you can create your own images
- They can be created in a file titled "Dockerfile" exactly like that
- **FROM** - Used to pull the base image you'd like to build off of. When choosing the tag, alpine is recommended because it makes your image sizes a lot smaller
- **RUN** - Allows you to run any command
- **COPY** - Used to copy files from a source to a destination which executes on the host instead of just the container like if you were to use cp with RUN. **CMD hostSrc containerDest**
- **ADD** - Similar to COPY, but it can auto-extract .tar files and you can download from URLs
- **CMD** - Defines the default command that should be executed when a container starts. Only one allowed per file
- **WORKDIR** - Sets the working directory for any commands that follow it. This is what you should look for in files when running **docker exec -it <container-name> /bin/sh**. If that doesn't work, use /bin/bash at the end instead
```
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
``` 
- After you have those two in your Dockerfile, change directory to where your file is and run **docker build --tag [imageName]:[imageTag] .**. The dot at the end is for the location to build
- It might also be important to have a docker ignore file for ignoring things like downloaded node modules or your own docker file. All you have to do is create a file with the name **.dockerignore** and place in any file names just as they're written into the file with no other syntax

## docker-compose

- You use a single YAML file to configure and maintain your application's services
- With a single command, you create and start all the services from your configuration
- To run it, simply do **docker-compose -f [dockerComposeFile.yml] up -d**. Can replace up with start if existing containers are stopped
- To stop and remove all the containers, run **docker-compose -f [dockerComposeFile.yml] down**. Can replace down with stop to only stop instead of removing
```yaml
version: '3.1' # This will be the latest docker-compose version
services: # This is where you will list all of your services/containers that you want to run
  mongodb: # Same as the --name flag on the command line for docker
    container_name: mongodbname # Another way of naming your container
    image: mongo # The image that you'd like to use
    ports: # Ports to run the container on
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
    depends_on: # Tells Docker that the specified service needs to be up and running before this one starts
      - "someOtherService"

  my-app:
    build: . # This will build our own image using everything in our current directory (The dot ".")
    ports:
      - 3000:3000
```





