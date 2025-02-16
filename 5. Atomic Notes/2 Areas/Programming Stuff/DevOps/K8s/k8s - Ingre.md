2024-12-01 21:31
Status: #baby
Tags: [[computer science]] [[k8s]]
## Main
## Setting the scene for Ingress
NodePorts only work on high port numbers (30000-32767) and require knowledge of node names or IPs. LoadBalancer Services fix this, but require a 1-to-1 mapping between an internal Service and a cloud load- balancer. This means a cluster with 25 internet-facing apps will need 25 cloud load-balancers, and cloud load- balancers aren’t cheap. They may also be a finite resource – you may be limited to how many cloud load-balancers you can provision.

Ingress fixes this by exposing multiple Services through a single cloud load-balancer.

![[Screenshot 2023-10-05 at 09.46.25.png]]

![[Screenshot 2023-10-05 at 09.48.52.png]]

two different hostnames (URLs) configured to hit the same load-balancer. An Ingress object is watching, and uses the hostnames in the HTTP headers to route traffic to the appropriate backend Service. This is an example of the HTTP host-based routing pattern, and it’s almost identical for path-based routing.


## References


