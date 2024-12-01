## Working with Pods
### Pod theory 
The atomic unit of scheduling on Kubernetes is the Pod. This is just a fancy way of saying apps deployed to Kubernetes always run inside Pods.

Some quick examples... If you deploy an app, you deploy it in a Pod. If you terminate an app, you terminate its Pod. If you scale an app up or down, you add or remove Pods.

The process of building and running an app on Kubernetes is roughly as follows:

1. Writeyourapp/code  
2. Packageitasacontainerimage  
3. WrapthecontainerimageinaPod 
4. RunitonKubernetes

#### Pods augment containers
On the augmentation front, Pods augment containers in all of the following ways.

• Labels and annotations  
• Restart policies  
• Probes(startup probes,readiness probes,liveness probes,and potentially more) 
• Affinity and anti-affinity rules  
• Termination control  
• Security policies  
• Resource requests and limits

#### Pods assist in scheduling
#### Pods enable resource sharing
Pods provide a shared execution environment for one or more containers. This shared execution environment includes things such as.
• Shared file system
• Shared network stack(IP address and ports...) • Shared memory
• Shared volumes
#### Static Pods vs controllers
There are two ways to deploy Pods.
1. Directly via a Pod manifest -> static Pods
2. Indirectly via a controller
#### Deploying Pods
1. Define it in a YAML manifest file
2. Post the YAML file to the api server
3. The API server authen and author the request
4. The config is valid
5. The scheduler deploys the Pod to a healthy node with enough available resources
6. The local kubelet monitors it
#### Pods and shared networking
Each Pod creates its own network namespace. This means a Pod has its own IP address, a single range of TCP and UDP ports, and a single routing table

![[Screenshot 2023-10-01 at 16.23.13.png]]

external access to the containers in the Pod on the left is achieved via the IP address of the Pod coupled with the port of the container you’re trying to reach. For example, 10.0.10.15:80 will get you to the main application container, but 10.0.10.15.5000 will get you to the supporting container.

Container-to-container communication within the same Pod happens via the Pod’s localhost adapter and a port number. For example, the main container in Figure 4.2 can reach the supporting container on localhost:5000.

#### The pod network
every Pod gets its own unique IP addresses that’s fully routable on an internal Kubernetes network called the pod network. The pod network is flat, meaning every Pod can talk directly to every other Pod without the need for complex port mappings. 
![[Screenshot 2023-10-01 at 16.25.32.png]]

#### Atomic deployment of Pods 
Pod deployment is an atomic operation. This means it’s all-or-nothing – deployment either succeeds or it doesn’t. You’ll never have a scenario where a partially deployed Pod is servicing requests. Only after all a Pod’s resources are running and ready will it start servicing requests.
#### Pod lifecycle
You define it in a declarative YAML object that you post to the API server and it enters the pending phase. It’s then scheduled to a healthy node with enough resources and the local kubelet instructs the container runtime to pull all required images and start all containers. Once all containers are pulled and running, the Pod enters the running phase. If it’s a short-lived Pod, as soon as all containers terminate successfully the Pod itself terminates and enters the succeeded state. If it’s a long-lived Pod, it remains indefinitely in the running phase.

#### Pod immutability
Pods are immutable objects. This means you can’t modify them after they’re deployed.
• When updates are needed, replace all old Pods with new ones that have the updates
• When failures occur, replace failed Pods with new identical ones
#### Pods and scaling
All Pods run a single application container instance, making them an ideal unit of scaling – if you need to scale the app, you add or remove Pods. This is call horizontal scaling.
You never scale an app by adding more of the same application containers to a Pod. Multi-container Pods are not a way to scale an app, they’re only for co-scheduling and co-locating containers that need tight coupling.

### Multi-container pods
#### Sidecar multi-container Pods
t has a main application container and a sidecar container. It’s the job of the sidecar to augment or perform a secondary task for the main application container. The previous example of a main application web container, plus a helper pulling up-to-date content is a classic example of the sidecar pattern – the “sync” container pulling the content from the external repo is the sidecar.
#### Adapter multi-container Pods
the helper container takes non- standardized output from the main container and rejigs it into a format required by an external system
NGINX logs being sent to Prometheus. Out-of-the-box, Prometheus doesn’t understand NGINX logs, so a common approach is to put an adapter sidecar into the NGINX Pod that converts NGINX logs into a format accepted by Prometheus.
#### Ambassador multi-container Pods
the helper container brokers connectivity to an external system. For example, the main application container can just dump its output to a port the ambassador container is listening on and sit back while the ambassador container does the hard work of getting it to the external system.
#### Init multi-container Pods
It runs a special init container that’s guaranteed to start and complete before your main app container. It’s also guaranteed to only run once.
### Hands-on with Pods
