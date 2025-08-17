2025-08-14 22:24
Status: #baby
Tags: [[k8s]]
## Main
**Pods are fundamental to running apps on Kubernetes**

The process of building and running an app on Kubernetes is roughly as follows:
1. Write your app/code
2. Package it as a container image
3. Wrap the container image in a Pod
4. Run it on Kubernetes

Kubernetes doesn’t allow containers to run directly on a cluster, they always
have to be wrapped in a Pod.

3 main reasons: 
1. Pods augment containers
2. Pods assist in scheduling
3. Pods enable resource sharing


	
## References