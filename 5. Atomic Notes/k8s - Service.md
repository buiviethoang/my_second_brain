2024-12-01 21:33
Status: #baby
Tags: [[computer science]] [[k8s]]
## Main
## Setting the scene
When Pods fail, they get replaced by new ones with new IPs. Scaling-up introduces new Pods with new IP addresses. Scaling down removes Pods. Rolling updates also replace existing Pods with new ones with new IPs. This creates massive IP churn and demonstrates why you should never connect directly to any particular Pod.
- a Kubernetes Service is a REST object in the API that you define in a manifest and post to the API server.
- every Service gets its own stable IP address, its own stable DNS name, and its own stable port.
- Services use labels and selectors to dynamically select the Pods to send traffic to.
## Service theory 
**Without services**

![[Screenshot 2023-10-05 at 08.53.35.png]]

**With services**
![[Screenshot 2023-10-05 at 08.54.23.png]]

Think of Services as having a static front-end and a dynamic back-end. The front-end, consisting of the IP, DNS name, and port, never changes. The back-end, comprising the list of healthy Pods, can be constantly changing.

### Labels and loose coupling

![[Screenshot 2023-10-05 at 08.56.09.png]]

the Service is providing stable networking to all three Pods – you send requests to the Service and it forwards them to the Pods. It also provides basic load-balancing.
### Services and Endpoint objects

he Service dynamically updates its list of healthy matching Pods. It does this through a combination of label selection and a construct called an Endpoints object.
Every time you create a Service, Kubernetes automatically creates an associated Endpoints object. The Endpoints object is used to store a dynamic list of healthy Pods matching the Service’s label selector.
### Accessing Services from inside the cluster
Kubernetes supports several types of Service. The default type is ClusterIP.
A ClusterIP Service has a stable virtual IP address that is only accessible from inside the cluster.
### Accessing Services from outside the cluster
- Nodeport
- LoadBalancer
![[Screenshot 2023-10-05 at 09.11.44.png]]
NodePort Services build on top of the ClusterIP type and enable external access via a dedicated port on every cluster node. We call this port the “NodePort"
LoadBalancer Services make external access even easier by integrating with an internet-facing load-balancer on your underlying cloud platform. You get a high-performance highly-available public IP or DNS name that you can access the Service from. You can even register friendly DNS names to make access even simpler – you don’t need to know cluster node names or IPs.
### Service discovery
Kubernetes implements Service discovery in a couple of ways:
1. DNS
2. Environment variables
Kubernetes clusters run an internal DNS service that is the centre of service discovery. Service names are automatically registered with the cluster DNS, and every Pod and container is pre-configured to use the cluster DNS. This means every Pod/container can resolve every Service name to a ClusterIP and connect to the Pods behind it.



## References


