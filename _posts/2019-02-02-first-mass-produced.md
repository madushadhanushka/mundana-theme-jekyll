---
layout: post
title:  "Kubernetes in Microservices World"
author: sal
categories: [ tutorial ]
image: https://hashnode.imgix.net/res/hashnode/image/upload/v1553077553650/FpwpRvSPX.jpeg?w=500&h=263&fit=crop&crop=entropy&auto=format,enhance&q=60
tags: [featured]
---
Handling large software which has multiple services is a tedious, time-consuming task for DevOps engineer. Microservices comes into the rescue DevOps from all these complicated deployment processes. In simply, each microservice in the system response to handle one specific task. The container can be used to deploy each of these micro-tasks as a unit of service. If you are not that familiar with Containers, read [this](https://hashnode.com/post/introduction-to-docker-life-cycle-cjsujgkbn002agvs1pcfx99lb) article to get to know about Docker, Which is the most popular and widely used container technology so far.

So far we have one container which has all required configurations and dependencies for one specific service. Single service always faces a common problem of a single point of failure. In order to avoid single point failure, we need to set up another service such that if one service is getting down, another service takes that load. Another requirement to have multiple containers for the same service is that, distributing the load between the services. This can be achieved by connecting multiple services through a load balancer. To maintain multiple containers which have multiple services with service replication is not that easy task to handle manually. To automate this process, Kubernetes comes to the rescue by providing the capability of container orchestration.
### What Kubernetes do?
Imagine you have an application which has multiple services and each of these services configured inside a container. Let assume these two services as Service A and Service B and Service A use Service B. Now we can represent services as follows.

![services.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1552746447509/Mk9Ql1dmR.jpeg)
When high availability required, then we need to scale the system so that each service have a copy of its own and run these copy in another node( separate physical/ virtual machine).

![services (1).jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1552746901189/QVAp0Uair.jpeg)
Here, load balancer used to distribute the load between servers. In this system, single point failure handled by routing traffic to other node if one node is getting down.

In lager system which has lots of nodes and services, hardware utilization may be not efficient since each of service requires different hardware requirements. Therefore hardwiring services into a specific node is not that efficient. Kubernetes provide an elegant way to solve this resource utilization issues by orchestrating container services in multiple nodes.

Kubernetes cluster maintains by the master which include scheduling applications, maintaining applications' desired state, scaling applications, and rolling out new updates. A node is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster. Node and master communicate with each other through the Kubernetes API.
A Kubernetes pod is a group of containers that are deployed together on the same host.

### Features of Kubernetes
Kubernetes provide multiple features so that application deployer can easily deploy and maintain the whole system.
- Container grouping using pod

A pod is a collection of containers and the unit of deployment in Kubernetes cluster. 
- Control replication

This component allows maintaining the number of replicated services that need to keep in Kubernetes cluster.
- Resource Monitoring

Health and the performance of the cluster can be measure by using add ons such as Heapster. This will collect the metrics from the cluster and save stats in InfluxDB. Data can be visualized by using Grafana which is ideal UI to analyze these data.
- Horizontal auto scaling

Heapster data also useful when scaling the system when high load comes into the system. Number of pods can be increase or decrease according the load of the system.
- Collecting logs

Collecting log is important to check the status of the containers. Fluentd used along with Elastic Search and Kibana to read the logs from the containers.

See you in next article to get hands-on experience of Kubernetes. Also you are welcome to follow me on [twitter](https://twitter.com/Dhanushkamadus2) to get to know more about tech news. Cheers :).
