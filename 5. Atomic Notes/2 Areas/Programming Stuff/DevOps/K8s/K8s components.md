2025-08-09 11:19
Status: #baby
Tags: [[k8s]]
## Main

### Kubernetes as a cluster

Kubernetes is like any other cluster – a bunch of machines to host applications. We call these machines “**nodes**”,
and they can be physical servers, virtual machines, cloud instances, Raspberry Pis, and more

A Kubernetes cluster is made of a **control plane** and **nodes**.
#### Control plane nodes
A Kubernetes control plane node is a server running collection of system services that make up the control plane
of the cluster. Sometimes we call them Masters, Heads or Head nodes

![[Pasted image 20230929213835.png]]


##### The API server
The API server is the Grand Central of Kubernetes. All communication, between all components, must go
through the API server. It’s important to understand that internal system
components, as well as external user components, all communicate via the API server – all roads lead to the API
Server.
##### The cluster store
The cluster store is the only stateful part of the control plane and persistently stores the entire configuration and
state of the cluster. As such, it’s a vital component of every Kubernetes cluster – no cluster store, no cluster.
##### The controller manager and controllers
The controller manager implements all the background controllers that monitor cluster components and respond
to events.
##### The scheduler
At a high level, the scheduler watches the API server for new work tasks and assigns them to appropriate healthy
worker nodes. Behind the scenes, it implements complex logic that filters out nodes incapable of running tasks,
and then ranks the nodes that are capable. The ranking system is complex, but the node with the highest ranking
score is selected to run the task.

#### Worker Nodes
Nodes are servers that are the workers of a Kubernetes cluster

At a high-level they do three things:
1. Watch the API server for new work assignments
2. Execute work assignments
3. Report back to the control plane (via the API server)

![[Pasted image 20250809112545.png]]

##### Kubelet
The kubelet is main Kubernetes agent and runs on every cluster node. In fact, it’s common to use the terms node
and kubelet interchangeably
When you join a node to a cluster, the process installs the kubelet, which is then responsible for registering it
with the cluster. This process registers the node’s CPU, memory, and storage into the wider cluster pool.
##### Container runtime
The kubelet needs a container runtime to perform container-related tasks – things like pulling images and starting
and stopping containers.
##### Kube-proxy
This runs on every node and is responsible for local cluster
networking. It ensures each node gets its own unique IP address, and it implements local iptables or IPVS rules
to handle routing and load-balancing of traffic on the Pod network

### Objects / Resources
#### Kubernetes DNS
The cluster’s DNS service has a static IP address that is hard-coded into every Pod on the cluster. This ensures
every container and Pod can locate it and use it for discovery. Service registration is also automatic. This means
apps don’t need to be coded with the intelligence to register with Kubernetes service discovery.
#### Pods
In the VMware world, the atomic unit of scheduling is the virtual machine (VM). In the Docker world, it’s the
container. Well… in the Kubernetes world, it’s the Pod.

![[Pasted image 20250809113345.png]]

It’s true that Kubernetes runs containerized apps. However, Kubernetes demands that every container runs inside
a Pod.
The point is, a Kubernetes Pod is a construct for running one or more containers. Figure 2.7 shows a multi-
container Pod.
![[Pasted image 20250809113516.png]]

#### Deployments
Most of the time you’ll deploy Pods indirectly via higher-level controllers. Examples of higher-level controllers
include Deployments, DaemonSets, and StatefulSets.
As an example, a Deployment is a higher-level Kubernetes object that wraps around a Pod and adds features
such as self-healing, scaling, zero-downtime rollouts, and versioned rollbacks.
Behind the scenes, Deployments, DaemonSets and StatefulSets are implemented as controllers that run as watch
loops constantly observing the cluster making sure observed state matches desired state

#### Services
Services bring stable IP addresses and DNS names to the unstable world of Pods.

=> *The Pod is the basic building-block that application containers run in. Deployments add self-healing, scaling and*
*updates. Services add stable networking and basic load-balancing.*
### Kubernetes as an orchestrator
Orchestrator is just a fancy word for a system that takes care of deploying and managing applications.

You start out with an app, package it as a container, then give it to the cluster (Kubernetes). The cluster is made
up of one or more control plane nodes and a bunch of worker nodes

You follow this simple process to run applications on a Kubernetes cluster.

1. Design and write the application as small independent microservices in your favourite languages.
2. Package each microservice as its own container.
3. Wrap each container in a Kubernetes Pod.
4. Deploy Pods to the cluster via higher-level controllers such as Deployments, DaemonSets, StatefulSets,
CronJobs etc

## References