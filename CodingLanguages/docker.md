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
- You will always have a base image that you will build from and you can pull this in with the **FROM** keyword
- Then wherever your dockerfile is, you're going to want to add the files in the directory to the base image with the **ADD** keyword
```
FROM nginx:latest
ADD . /user/share/nginx/html
``` 





