2025-08-09 11:00
Status: #baby
Tags: [[computer science]] [[k8s]]
## Main

### Background
Kubernetes is an **application orchestrator**. For the most part, it orchestrates containerized **cloud-native** **microser-**
**vices** apps
#### Orchestrator
An orchestrator is a system that **deploys** and **manages** applications. It can deploy your applications and
dynamically respond to changes. For example, Kubernetes can:
• Deploy your application
• Scale it up and down dynamically based on demand
• Self-heal it when things break
• Perform zero-downtime rolling updates and rollbacks
• Lots more…
And the best part about Kubernetes… it does all of this without you having to supervise or get involved. Obviously,
you have to set things up in the first place, but once you’ve done that, you sit back and let Kubernetes work its
magic
#### Containerised app

A containerized application is an app that runs in a container

Before we had containers, applications ran on physical servers or in virtual machines. Containers are just the
next iteration of how we package and run apps. As such, they’re faster, more lightweight, and more suited to
modern business requirements than servers and virtual machines.
Think of it this way.
• Apps ran on physical servers in the open-systems era (1980s and 1990s)
• Apps ran in virtual machines in the virtualisation era (2000s and into the 2010s)
• Apps run in containers in the cloud-native era (now)

While Kubernetes can orchestrate other workloads, such as virtual machines and serverless functions, it’s most
commonly used to orchestrate containerised apps.
#### Cloud-native app
A **cloud-native** application is one that’s designed to meet cloud-like demands of auto-scaling, self-healing, rolling
updates, rollbacks and more.

It’s important to be clear that cloud-native apps are not applications that will only run in the public cloud. Yes,
they absolutely can run on public clouds, but they can also run anywhere that you have Kubernetes, even your
on-premises datacenter.
So, cloud-native is about the way applications behave and react to events.
#### Microservices app

A microservices app is built from lots of independent small specialised parts that work together to form a
meaningful application

For the most part, each microservice runs as a container. Assuming this e-commerce app with the 6 microservices,
there’d be one or more web front-end containers, one or more catalog containers, one or more shopping cart
containers etc.


=> *Kubernetes deploys and manages (orchestrates) applications that are packaged and run as containers (container-*
*ized) and that are built in ways (cloud-native microservices) that allow them to scale, self-heal, and be updated*
*in-line with modern cloud-like requirements.*

### Why? 
Kubernetes enables two things Google and the rest of the industry needs.
1. It abstracts underlying infrastructure such as AWS
2. It makes it easy to move applications on and off clouds

### Kubernetes and Docker

Kubernetes and Docker are complementary technologies.
Docker has tools that build and package applications as container images. It can also run containers. Kubernetes
can’t do either of those things. Instead, Kubernetes operates at a higher level providing orchestration services
such as self-healing, scaling and updates.

It’s common practice to use Docker for build-time tasks such as packaging apps as containers, but then use a
combination of Kubernetes and Docker to run them. In this model, Kubernetes performs high-level orchestration
tasks such as self-healing, scaling and rolling updates, but it needs a tool like Docker to perform low-level tasks
such as starting and stopping containers.

![[Pasted image 20230929205628.png]]

Docker isn’t the only container runtime Kubernetes supports. In fact, Kubernetes has a couple of
features that abstract the container runtime and make it interchangeable:

Multiple run-time containers: 
1. The Container Runtime Interface (CRI) is an abstraction layer that standardizes the way 3rd-party
container runtimes work with Kubernetes.
2. Runtime Classes allows you to create different classes of runtimes. For example, the gVisor or Kata
Containers runtimes might provide better workload isolation than the Docker and containerd runtimes.

## References