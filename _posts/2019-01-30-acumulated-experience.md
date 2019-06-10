---
layout: post
title:  "Introduction to The Docker Life Cycle"
author: sal
categories: [ Jekyll, tutorial ]
image: https://hashnode.imgix.net/res/hashnode/image/upload/v1551680604565/lOt0NNEiB.jpeg?w=1600&h=840&fit=crop&crop=entropy&auto=format,enhance&q=60)
---

Maintaining a large software application is not that easy task since it may have lots of dependencies and OS related configurations. What if you can create an OS image which already contains required libraries and configurations that needs to run your application? Then that would be really easy for software deployer to deploy their application easily on a cloud without doing a tedious task of setting up an OS environment. One possible solution to overcome this problem is to use a Virtual Machine. You can install all libraries, setting up configurations and take an image. When you need to deploy the application, you can simply start the machine with that image. A VM provide complete low-level machine to run an Operating System. But it does not perform faster due to VM's operational overhead. In this case Container technology comes to rescue.

### Containers vs VMs

![1_JZRIfFqfVuG7TAUOmJACHw.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1551545546828/lw1W7f2Xs.png)

VM is nothing more than a computer that executes a program. VM is running on top of software which called Hypervisor. Here, the physical computer is known as the Host machine and the VM that running top of Hypervisor known as Guest Machine.
Containers act the same as the VM, but the difference is that Containers use host machine OS instead of hardware visualization to run as a VM. Each container has its own userspace and runs on top of host OS. This makes container much faster than VMs.

Another thing about the docker is that you can keep docker images in a central repository. This repository is known as Docker Registry. Docker Registry works the same as GIT Repository. You can commit your current container as an image and push it into the Docker Registry. You can also pull images back from the Docker Registry. [Docker Hub](https://hub.docker.com/) is a one such a Docker Registry that you can keep images. Following services are also widely used as Docker Registries.
1. [Quay](https://quay.io/)
2. [Google Container Registry](https://cloud.google.com/container-registry/)
3. [AWS Container Registry](https://aws.amazon.com/ecr/)

A container can be compared with a process in OS. A process is an instance of a computer program that is being execting. A process can have multiple thread running. Containers are also working same as a process, but the difference is that Containers are processing with their full environment. Containers can have the following states.
- **Created**: A container that has been created. but not started
- **Restarting**: A container that is in the process of being restarted
- **Started**: A currently running container
- **Paused**: A container whose processes have been paused
- **Exited**: A container that ran and completed 
- **Dead**: A container that the daemon tried and failed to stop (usually due to a busy device or resource used by the container)

![dockerlife.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1550292571285/2T44LpBlf.jpeg)

### Common Commands in Docker Life Cycle
Here, below are the list of commands that used to change the docker states.
```
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
Pulls an image from a remote docker hub and saves it in your local machine. This command works the same as Git pull command. 

```
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
```
This command creates a new Docker container by a specified image.

```
docker start [OPTIONS] CONTAINER [CONTAINER...]
```
This command used to start an exited or newly created container into the running state.

```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

This command creates a new container and runs the image in a newly created container. Both of the "docker create" and "docker start" command can be executed by this single command.

```
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```
This command stops the running container. This will change the container status from running to excited.

```
docker pause CONTAINER [CONTAINER...]
```
This command suspends the running process in running container by issuing SIGSTOP command.

```
docker unpause CONTAINER [CONTAINER...]
```
This command gets back suspended process into the running state.

Read more about docker command with examples in my previous post.

%[https://hashnode.com/post/commonly-used-docker-commands-cjrz18xrn00bse2s22w6y3jjv]

