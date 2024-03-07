Kubernetes

Containers 
Isolated environments, running on the same OS/VM
Image: Update the image, not the container since the container should be stateless. Image is a template for a container (containers are running instances of images). Prepackaged.E.g. If there is a patch required, update package on the image, then push out the new image to replace the old containers. (images are templates for a container - e.g. can container binaries + dependencies + custom code)
Stateless - e.g. logs from a container (e.g. DB) will be transferred to a persistent storage
Not tightly coupled
If need to scale, can replicate more containers within the same VM or can spin up new VM. Previously, in monolithic app, if we needed scalability would have to increase OS resources of the VM or clone the VM.
Still need to deploy a LB


Two types of Docker
Docker runtime (layer on top of OS)
Docker swarm - orchestration (but we use kubernetes)

Docker
Deploy docker runtime engine 

Docker version
Docker images (images)
Docker ps (containers)
Docker pull <image name> (download image from online)
Docker run <image name> (download image and run from online)

Kubernetes

Pods are the almost equivalent concept of a container in Kubernetes, pods are the lowest ‘level’. Recommended that pod:container ratio is 1:1, but you can have more than one container in a pod if needed. 
There is no concept of container in Kubernetes. Think of pod as a wrapper around container
Pod --M:1--> Node --M:1→ Cluster
Cluster can be broken off based on sensitivity of the cluster
You can run linux pod/container on a Windows OS/kernel (since Windows has compatibility), but cannot run Windows container on Linux
You can (and should) have more than one master node
Cluster will decide which node to deploy the pod to, you cant choose 
Declarative nature of kuberenetes mean it only cares about end state - e.g. if file says it wants to create 3 pods, but 3 pods already exist then it wont create it.
Communicate to master or cluster , not to the node
If master is down, clusters will still run but no communication
You cant edit labels of existing pods - so best to delete? Then re-deploy
To scale up, there are 2 options - scale command (1 off) or update the config file
Replicaset checks on an ongoing basis that criteria is being matched
Pods cant be renamed
Pods - single instances of applications
Replicaset - multiple POD instances
Deployments - orchestrate application management (multiple replicasets)
Default deployment strategy is to create new instances, THEN delete old instances. However at the end of the day, may still need planned outage (e.g. if has active user sessions)

Networking
Assign unique IP address to pods/clusters/node
No IP management at pod layer - since pods always spun down/up
Pods get IP address within subnet range of cluster




Azure Kubernetes Service
Within an Azure region (e.g. AU East), you can have multiple availability zones (physical DC within regions). When you deploy a cluster to a region with >1 AZs, the nodes can be spread out across the AZs. if one of the AZs goes down, the node thats meant to be on there will be moved/spun to another AZ. If the AZ comes back up, the original node will move back.

Ingress
Load balancer (RBA uses azure application gateway)


Networking
https://cloud.google.com/architecture/microservices-architecture-refactoring-monoliths 
