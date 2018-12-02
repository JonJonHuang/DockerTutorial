# Getting Started with Docker
Docker provides a platform to develop, deploy, and run applications with containers.
Key concepts covered 
  - What is a container?
  - How to launch a container?
  - Where does the container run?
  - Docker vs virtual machines
  - Setting up docker environment

### What is a container?
A [Linux® container] is a set of processes that are isolated from the rest of the system. Linux containers are flexible, lightweighted, portable, interchangeable, and scalable. This makes them much faster than other development pipelines that depend on replicating traditional testing environments. The utilization of Linux containers to deploy applications is named as containerization.
### How is a container launched?
Containers are launched by running an image. An image is an executable package that includes everything (code, libraries, configuration files, etc.,) needed to run an application.
A container is a runtime instance of an image with state, or a user process. The list of running containers can be viewed by using docker ps command
### Where does the container run?
A container runs a discrete process natively on Linux by sharing the kernal of the host machine with other containers. These containers do not take any additional memory to run, making it lightweight.
### Docker vs Virtual Machine
| Docker container | Virtual Machine |
| ------ | ------ |
| Docker containers support OS virtualization | VM supports hardware virtualization |
| The application feels that it has a complete instance of an OS | Gives feel like it is a physical machine in which we can boot any OS |
| The containers running share the host OS kernel| VMs have their own OS files |
| It runs a discrete process, taking no more memory than any other executable, making it lightweight | VMs provide an environment with more resources than most applications need.|

![N|Solid](https://i.ytimg.com/vi/TvnZTi_gaNc/maxresdefault.jpg)
### Setting up Docker environment
Install a required version of Docker Community Edition (CE) or Enterprise Edition (EE) on a supported platform fron [here].

Ensuring correct version..
```sh
$ docker --version
Docker version 17.12.0-ce, build c97c6d6
```
View installation details..
```sh
$ docker info
Containers: 0
Running: 0
Paused: 0
Stopped: 0
Images: 0
Server Version: 17.12.0-ce
Storage Driver: overlay2
...
```
Testing succesful installation..
1. Run a simple docker image file
    ```sh
    $ docker run hello-world
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    ca4f61b1923c: Pull complete
    Digest: sha256:ca0eeb6fb05351dfc8759c20733c91def84cb8007aa89a5bf606bc8b315b9fc7
    Status: Downloaded newer image for hello-world:latest
    
    Hello from Docker!
    This message shows that your installation appears to be working correctly.
    ...
    ```
2. List the hello-world image that was downloaded to your machine:
    ```sh
    $ docker image ls
    ```
3. Display the containers. This should display the recent hello-world container
    ```sh
    $ docker container ls --all
    CONTAINER ID     IMAGE     COMMAND     CREATED          STATUS
    54f4984ed6a8  hello-world  "/hello"  20 seconds ago   Exited (0)
    ```
[Linux® container]: <https://www.redhat.com/en/topics/containers>
[here]: <https://docs.docker.com/install/>
