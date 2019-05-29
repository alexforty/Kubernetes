# Kube Proxy.

- Within a kubernetes cluster every pod can reach every other pod.
- This is accomplished by deploying a POD networking solution to the cluster. 
- A POD network is an internal virtual network that spans across all nodes in the cluster to which all PODs connect.
- Through this network PODs are able to communicate with each other.
- There are many solutions available for deploying such a network.

## Example 

- a simple 2 node 1 master cluster is deployed
- a web application deployed on the first node and a database application deployed on the second.
- The web app can reach the database, simply by using the IP of the database POD.
- due to PODs being inherently transiet,there is no guarantee that the IP of the database POD will always remain the same.
- a better way for the web application to access the database is using a service. 
    - a service is created to expose the database application across the cluster.
    - The web application can now access the database using the name of the service.
    - The service also gets an IP address assigned to it, therefore, whenever a pod tries to reach the service using its IP or name it forwards the traffic to the pod.

- But:
    - What is this service? 
    - How does it get an IP?
    - Does the service join the same POD Network?

The service cannot join the pod network because the service is not an actual thing i.e. it is not a container like pod so it doesn't have any interfaces or an actively listening process.

It is a virtual component that only lives in the cabinet as memory.

however the service should be accessible across the cluster from any node.

_So how is that achieved?_

Kube-proxy is a process that runs on each node in the kubernetes cluster. Its job is to look for new services and every time a new service is created it creates the appropriate rules on each node to forward traffic to those services to the backend pods. e.g. using IPTABLES rules.

In example it creates an IP table rule on each node in the cluster to forward traffic heading to the IP of the service  to the IP of the actual pod. So how kube-proxy configure the service

We discuss a lot more about networking and services kube-proxy and POD networking.

Later in this course again we have a large section just for networking.