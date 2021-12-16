# kubernetes-notes
## Overview
## Introduction to K8S
- What is Kubernetes
- K8S Architecture
- Main K8s Components
- Minikube and Kubectl 
- Main Kubectl commands & K8s CLI
- K8S yaml
## Advanced Concepts
- K8s Namespaces
- K8s Ingress
- Helm -> Package Manager
- Volumes 
- K8S Stateful Set
- K8S Services

---
### What Kubernetes is?
Open source container orchestration tool
Helps you manage containerized applications

Trend from Monolith to Microservices
- High Availability or no downtime
- Scalability or high performance
- Disaster recovery backup and restore
---
### Kubernetes Components

**Node**
- Worker Node VM or 

**Pod** 
- Smallest unit of K8s
- Abstraction over container
- Usually 1 application per pod
- Each pod gets its own IP address (New IP address on re-creation)

> You only interact with kubernetes layer

**Service** 
- Permanent IP adress (pod own its service - even if pod dies service is up)

**Ingress**
- Service's external access point

**ConfigMap**
- external configuration of your application (dont put sensitive info use secret)

**Secret**
- like as config map
- used to store secret data
- base64 encoded

> The built-in security mechanism is not enabled by default

**Volumes**
- storage on local machine (node)
- or remote, outside of the k8s cluster

> K8s doesn't manage data persistance

> REPLICATE EVERYTHING

**StatefulSet**
- for STATEFUL apps or databases
- mongod mysql etc.

> DB are often hosted outside of k8s cluster
---
### Kubernetes Architecture

- each Node has multiple Pods on it
- 3 processes must be installed on every node
- worker nodes do the actual work

Worker machine (3 processes)

1. container runtime
2. kubelet - interacts with both the container and node
3. kube-proxy - low overhead communication - smart network

> Managing processes are done by Master Nodes

Master machine (4 processes)
1. api server - (cluster gateway) (acts as a gatekeeper for authentication)
2. scheduler - scheduler just decides on which node new pod should be scheduled
3. controller manager - detect cluster state changes
4. etcd - key value store of a cluster state - clusterbrain


## Minikube and Kubectl

Layers of abstraction
- Deployment manages a
- ReplicaSet manages a
- Pod is an abstraction of 
- containers

## Kubernetes Config YAML

3 parts
1. metadata
2. specification
3. status (desired and actual state) (created by kubernetes)

Where does K8S gets the actual status
- etcd store them
  
> kubectl get pod -o wide

> get status kubectl get deployment nginx-deployment -o yaml

## Kubernetes Namespaces

- Organise resources in namespaces
- Virtual cluster inside a cluster

4 Namespaces per default
> kubectl get namespaces
1. kube-system
   - do not create or modify in kube-system
   - system processes
   - master and kubectl processes
2. kube-public
   - publicely accesible data
   - a configmap, which contains cluster information
   - > kubectl cluster-info
3. kube-node-lease
   - heartbeats of nodes 
   - each node lease object in namespace
   - determines the availability of a node
4. default
   - 

Why to use namespaces?
- no overview :(
- resources grouped in namespaces (database, montioring, elastic stack kibana etc., nginx-ingress)
- should not use smaller projects

> avoid such kind of conflicts team namespaces

- staging development namespaces
- both use elastic and database namespace
  
- Blue/Green Deployment (with same resources, no need to seperate)

- access and resource limits on namespaces
- ProjectA and ProjectB namespaces isolated environment
- Limit CPU, RAM, Storage per NS (Resource quota A, B)

NOTES:
- you cant use ProjectA configmap inside ProjectB
- you should create for each
- on database namespace mysql-service for instance configmap definition is mysql-service.database (database is a namespace)

- volume can't be craeted within a namespace

> kubens for changing namespaces (kubectx)

### What is INGRESS

- my-app-pod -> my-app-service (external IP, not final product)-> my-app-ingress (domain name)

- You need an implementation for Ingress -> Ingress Controller (Ingress Controller Pod)
- many-third party implementations? K8s Nginx Ingress Controller - inside k8s
- ProxyServer ---> Ingress Controller Pod

- add two rules for subdomains etc.mydomain something.mydomain
- add two paths for to serve on same domain mydomain/etc mydomain/something

- configuring TLS certificate
- spec tls and secretName secret refet secret-tls in kubernetes tls certificate base64encoded cert and key
- 



