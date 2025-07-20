## Docker

## What is Docker

- Docker is a tool for running applications in an isolated environment, similar to a virtual machine
- Docker uses containers which are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in user spaces.

## Images

- An image is a template for creating an environment of your choice
- You can also keep snapshots/versions of your images so in case you find an error in one, you can simply go back to a different version whenever
- Has everything you need to run your apps
- You can create your own images or you can find them publicly online at **hub.docker.com** where you can then do **docker pull [image]**

## Containers

- A container is simply a running instance of an image







