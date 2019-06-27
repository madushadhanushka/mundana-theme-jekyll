---
layout: post
title:  "Introduction to the Envoy Proxy Load Balancing"
author: dhanushka
categories: [ devops ]
image: //hashnode.imgix.net/res/hashnode/image/upload/v1561312457269/G5Pz1-Ghi.jpeg
---
Load balancing is a common term for a devops engineer. When huge of traffic comes into to your system, you need to find out a way to scale the system so that it can handle it properly. One solution is to increase the performance of the running single node. Another solution is to add more nodes and distribute the work among these nodes. Having many node have another added advantage of high availability. Load balancers used to distribute the traffic among the worker nodes.

Envoy proxy is a proxy service that used in latest trending concept that known as Service Mesh. We will see the load balancing aspect of the Envoy Proxy in this blog post.

## Load Balancers

![loadbalancer.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1561200701337/6m8S99wcO.jpeg)

Load balancers is an endpoint that listen to the request that coming into the computation cluster. When request comes into the Load balancer, it check for available worker nodes and distribute request among worker nodes. Load balancers do following things.
- Service Discovery: Check available worker nodes
- Health check: Regularly inspect worker nodes health.
- Load balancing: Distribute the request between the worker nodes.

## Proxy
Proxy is an intermediary component that exist between two endpoints. Proxy service take client request and forward it to the destination server. There are two types of proxies. Forward proxy and Reverse Proxy. Instead of sending request directly to the endpoint, we can also send it through a proxy. This type of proxy known as Forward proxy. Forward proxy commonly used to bypass the firewall restrictions and access to blocked websites.  

Revers proxy is a type of a proxy service that take incoming client request and forward it to the server that can fulfill it. The result will be rout back to the client. Addition to that, proxy also provide more control over the client request. It can also cache the request and speedup the network performance. Reverse Proxy used to
- To enable indirect access when a website disallows direct connections as a security measure.
- To stream internal content to Internet users.
- To allow for load balancing between severs.
- To disable access to a site.

## Load balancing topologies

Proxy sitting between client and backend endpoint. Load balancing can be divided into following topologies based on the place where proxy service placed.

### Middle Proxy

![middle proxy.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1561205086390/LSqMUbxzw.jpeg)

All client request comes into the the middle proxy. Middle proxy rout request into the worker node. This type of load balancers are simple and straight forward.

### Embedded Client Library


![embeddedlibrary.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1561205823453/R5t8rUG_s.jpeg)

The biggest problem in the Middle Proxy is that, Single point failure. If Middle Proxy server get down, then client services unable to access backend services.
In this type of proxy, instead of central load balancer, load balancing done by the client it self. This kind of system can implemented by using gRPC libraries.

Growing complexity become a problem in this type of load balancers. Also, developer need to install load balancing component for each of the service.

### Side Car Proxy

![embeddedlibrary (1).jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1561210903166/SeuzlneW7.jpeg)

The biggest problem in Embedded Client Library is that the complexity of building communication component for each of the services. With the recent trend of using container technology, Client Library separated into the containers. So, there is no programming languages lock in while developing decentralized load balancers. This is know as Side Car. This type of proxy service implementation known as Service Mesh. Side Car responsible to rout client request into the appropriate backend service.

Envoy is high performance revers proxy written in C++ language by Lyft. Envoy used to interconnect services in Service Mesh. Here follow are common terminology that used by Envoy proxy.

- Host: An entity capable of network communication.
- Downstream: Hosts that send request to the envoy proxy.
- Upstream: Host that receive request from the envoy proxy.
- Listener: Named network location that can connect to an envoy proxy through a downstream.
- Cluster: Cluster is group of logically same upstream host that envoy can connect. Envoy can discover cluster by using service discovery.

## Front Envoy Proxy
Aport from Side Car proxy, Envoy can be configure as Front envoy proxy as well. Front proxy configured as primary load balancer to the request coming in from the public internet. This proxy also know and edge proxy. Overall architecture of Service Mesh would be like follows.

![proxymesh.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1561216275915/eEMY3ilcZ.jpeg)

Here, front proxy used as load balancer for the incoming internet traffic. Here TLS termination also perform.  Then request rout to the relevant services through side car proxies. Service mesh can detect available services through service discovery. It also provide circuit brake features to handle fail overs. Collectively, Envoy provide whole bunch of features to implement a Service Mesh.

## Types of Load Balancers in Envoy Proxy
When proxy need to acquire connection to host in upstream cluster, the cluster manager use following polices to rout traffic.

- Round Robbin
Rout load to each of the worker nodes(upstream host) circular order. All worker node consider as same and all node get same amount of load.

- Random
Select worker node by random and rout the traffic. This is know to be perform better than Round Robbin policy.

- Weighted Least Request
This policy based on the number of connection that are keep while loading balance. Assume there are two worker nodes with same specs. Due to some reason first worker node take longer time to response. So it also have to keep it connection to first worker node longer than second node. In this scenario, load balancer can put more weight on second worker node rather sending traffic into the first node.

- Original Destination
This type of load balancer used when a given connection needs to connect to some particular upstream host. host selected by reading client's meta data.

Other than load balancing, Envoy also provide following feature to implement Service Mesh.
- Dynamic service discovery
- TLS termination
- HTTP/2 and gRPC proxies
- Circuit breakers
- Health checks
- Staged rollouts with %-based traffic split
- Fault injection
- Rich metrics

We will go through each of these features in next article. This article is to give you the basic introduction about Envoy Proxy and how it do Load Balancing. See you in another article. Cheers :)

References
-  [https://www.envoyproxy.io/docs/envoy/v1.5.0/intro/arch_overview/load_balancing](https://www.envoyproxy.io/docs/envoy/v1.5.0/intro/arch_overview/load_balancing)
- [https://www.jscape.com/blog/load-balancing-algorithms](https://www.jscape.com/blog/load-balancing-algorithms)
- [https://blog.envoyproxy.io/introduction-to-modern-network-load-balancing-and-proxying-a57f6ff80236](https://blog.envoyproxy.io/introduction-to-modern-network-load-balancing-and-proxying-a57f6ff80236)