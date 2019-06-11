---
layout: post
title:  "Commonly Used Docker Commands"
author: dhanushka
categories: [ devops]
image: https://hashnode.imgix.net/res/hashnode/image/upload/v1549819815002/D8Wzk68RA.png?w=1600&h=840&fit=crop&crop=entropy&auto=format,enhance&q=60
tags: [featured]
---
In this post, we are looking into some commonly used docker commands.

## `docker pull`

```
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
This command pulls an image from a remote docker hub and saves it in your local machine. This command works same as Git pull command. As an example, you can pull an Ubuntu image from docker hub by executing the following command.

`docker pull ubuntu`

You can specify the version/tag of the image name by adding a colon(:) mark at the end of the image name. For an example, to pull the latest Ubuntu, you can execute the command as follows.

`docker pull ubuntu:latest`

## `docker images`

```
docker images [OPTIONS] [REPOSITORY[:TAG]]
``` 
You can see what are the available docker images by executing this command. To get all available docker images, run

`docker images`

## `docker ps`

```
docker ps [OPTIONS]
```

You can use this command to list the containers. Following command can be used to list all the containers.

`docker ps -a`

Here you can see the current status of the containers. Containers can be in one of the following statuses.

- created
- restarting
- running
- removing
- paused
- exited
- dead

## `docker create`

```
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
```
This command creates a new Docker container by specified image as example mention below.

`docker create ubuntu`

once you created a new Docker container it moves its status to "created" status.

## `docker start`

```
docker start [OPTIONS] CONTAINER [CONTAINER...]
```

This command can be used to start an exited container.

`docker start 3a09b2588478`

Here you need to define the container id that needs to start with the docker start command. Both create and start command can be executed by a single command by using the docker run command as follows.

## `docker run`

```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

This command creates a new container and runs the image in the newly created container. Example docker runs for Ubuntu image as follows.

`docker run --name UbuntuImage -it ubuntu`

here "-it" option allows you to connect to the container from your terminal. You can set a name for the container by setting value for "--name" option.

## `docker attach`

```
docker attach [OPTIONS] CONTAINER
```

This command let you attach local standard input, output and error stream to run a container. Here, the container should be in the running state in order to run this command.

## `docker stop`

```
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```
This command stops the running container. This will change the container status from running to excited. You can add docker container id at the end of the docker stop command as follows.

`docker stop 3a09b2588478`

Docker stop command sends SIGTERM signal to the container to stop the container gracefull. If the container cannot be stoped in timeout it sends SIGKILL signal to the container and stops the container. Alternatively, you can use the "docker kill" command to stop containers forcefully. 

## `docker rm`

```
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

This command removes container completely from your computer. So be careful when using this command. Example command as follows.

`docker rm 3a09b2588478`

Have a question? Put a comment down below :)