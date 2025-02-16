2024-12-01 21:34
Status: #baby
Tags: [[computer science]] [[k8s]]
## Main
There are two major components to service discovery
1. Registration
2. Discovery
## Service registration
Service registration is the process of an application posting its connection details to a service registry so other
apps can find it and consume it.
![[Pasted image 20231006212809.png]]

1. Kubernetes uses its internal DNS as a service registry
2. All Kubernetes Services automatically register their details with DNS
Kubernetes provides a well-known internal DNS service that we usually call the **“cluster DNS”.**

It’s implemented in the **kube-system**
Namespace as a set of Pods managed by a Deployment called **coredns**

The process of service registration looks like this:
1. You post a new Service manifest to the API server
2. The request is authenticated, authorized, and subjected to admission policies
3. The Service is allocated a stable virtual IP address called a ClusterIP
4. An Endpoints object (or EndpointSlice) is created to hold a list of healthy Pods matching the Service’s
label selector
5. The Pod network is configured to handle traffic sent to the ClusterIP (more on this later)
6. The Service’s name and IP are registered with the cluster DNS

We mentioned earlier that cluster DNS is a Kubernetes-native application. This means it knows it’s running on
Kubernetes and implements a controller that watches the API server for new Service objects.
Any time it observes
one, it automatically creates the DNS records mapping the Service name to its ClusterIP. This means apps, and
even Services, don’t need to perform their own service registration – the cluster DNS does it for them.

At this point, the Service’s front-end configuration (name, IP, port) is registered with DNS and the Service can
be discovered by apps and clients.
### The Service back-end
Now the Service’s front-end is registered and can be discovered by other apps, the back-end needs building so there’s something to send traffic to
This involves maintaining a list of healthy Pod IPs the Service will load-
balance traffic to.
### Summarising service registration

## Service discovery
## Service discovery and namespaces
## Troubleshooting and service discovery
## References


