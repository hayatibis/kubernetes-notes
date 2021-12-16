# kubernetes-notes
### Overview
#### Introduction to K8S
- What is Kubernetes
- K8S Architecture
- Main K8s Components
- Minikube and Kubectl 
- Main Kubectl commands & K8s CLI
- K8S yaml
#### Advanced Concepts
- K8s Namespaces
- K8s Ingress
- Helm -> Package Manager
- Volumes 
- K8S Stateful Set
- K8S Services


##### What Kubernetes is?
Open source container orchestration tool
Helps you manage containerized applications

Trend from Monolith to Microservices
- High Availability or no downtime
- Scalability or high performance
- Disaster recovery backup and restore

##### Kubernetes Components

**Node**
Worker Node VM or 

**Pod** 
Smallest unit of K8s
Abstraction over container
Usually 1 application per pod
Each pod gets its own IP address (New IP address on re-creation)

> You only interact with kubernetes layer

**Service** 
Permanent IP adress (pod own its service - even if pod dies service is up)

**Ingress**
Service's external access point

**ConfigMap**
external configuration of your application (dont put sensitive info use secret)

**Secret**
like as config map
used to store secret data
base64 encoded

> The built-in security mechanism is not enabled by default

**Volumes**
storage on local machine (node)
or remote, outside of the k8s cluster

> K8s doesn't manage data persistance

> REPLICATE EVERYTHING

**StatefulSet**
for STATEFUL apps or databases
mongod mysql etc.

> DB are often hosted outside of k8s cluster

##### Kubernetes Architecture












