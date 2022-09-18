# Kubernetes

## What's kubernetes

An open-source, flexible container orcherstration system for automating software deployment.

## Main features

- Automated rollout and rollback.
- Automated load balancing and service discovery.
- Storage orchestration.
- Self-healing -> Automated restarts (livenessProbe/readinessProbe).
- easily Scales horizontally, can be automated.
- Secret and configMap managment.

## Architecture

At a high level a k8s cluster is composed of many nodes.
A node is a physical machine or virtual machine that is acknowledge as part of a cluster.
A node is either a control-plane node, previously known as master node, or node, previously known as worker node.

A common k8s cluster has the following components:

- one or more control-plane nodes.
- one or more worker nodes.
- a distributed key-value store, like **etcd**.

### Control plane

Controls the cluster and is the entrypoint for every admin task (e.g. update deployment).
For fault tolerance purposes, there can be more than one master node in the cluster.
To manage the cluster state, Kubernetes uses **etcd** and all control-plane nodes connect to it. 

#### Control plane components

1. [kube-apiserver](#kube-apiserver)
2. [etcd](#etcd)
3. [kube-scheduler](#kube-scheduler)
4. [kube-controller-manager](#kube-controller-manager)
5. [cloud-controller-manager](#cloud-controller-manager)

#### kube-apiserver

The (RESTful) API server exposes the Kubernetes API and is the frontend for the Kubernetes control plane.
It scales horizontally, if necessary.

#### ETCD

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd) is a distributed key-value store that can be part of the control-plane node and persists all the cluster's data.

#### kube-scheduler

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler) is control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.

#### kube-controller-manager

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager) Control plane component that runs controller processes.

Some types of these controllers are:

- Node controller: Responsible for noticing and responding when nodes go down.
- Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
- Endpoints controller: Populates the Endpoints object (that is, joins Services & Pods).
- Service Account & Token controllers: Create default accounts and API access tokens for new namespaces.

#### cloud-controller-manager

A Kubernetes control plane component that embeds cloud-specific control logic. 
The cloud controller manager lets you link your cluster into your cloud provider's API.

### Node

nodes, previously known as worker nodes, are virtual of physical machines that run pods.
Pods are scheduled on nodes, which have the necessary tools to run and connect them.

#### Node components

1. [kubelet](#kubelet)
2. [kube-proxy](#kube-proxy)
3. [container runtime](#container-runtime)

#### kubelet

[kubelet](https://kubernetes.io/docs/concepts/overview/components/#kubelet) is a node component that manages containers and pods
and checks that pods are healthy.
It communicates with the control plane and with the Container runtime, using CRI (Container runtime interface).

#### kube-proxy

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy) is a node component that controls the routing of requests to pods
using the service specified.

####  Container runtime

[Container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime) component of nodes, is the software that is responsible for running containers.
Kubernetes supports container runtimes that implements of the Kubernetes CRI (Container Runtime Interface).

##### Container runtime examples

- containerd, used by docker
- CRI-O, built specifically for k8s

### Node network

every pod gets its unique IP
Inside a Pod, containers share the network namespaces (Linux feature), so that they can reach to each other via localhost.

#### linux namespaces

A Linux namespace is a Linux kernel feature that isolates and virtualizes system resources. 
Processes which restricted to a namespace can only interact with resources or processes that are part of the same namespace.

---

## K8S primitives

K8s uses objects to model its clusters.
Every object is a part/aspect of a cluster that is configurable.
Generally yaml files are used to store entities and best practice is to use VCS (git) to store the configurations.


## K8s objects

### Namespace

namespaces provides a mechanism for isolating groups of resources within a single cluster. 
Names of resources need to be unique within a namespace, but not across namespaces.
Namespace-based scoping is applicable only for namespaced objects.
Namespaces are a way to divide cluster resources between multiple users or deployment environments.

#### Create namespace

```bash
kubectl create namespace <NAME-HERE>
```

### Labels

Labels are key/value pairs that are attached to objects, such as pods or deployments. 
Labels are intended to be used to specify identifying attributes of objects.
Labels can be used to organize and to select subsets of objects.

#### Select by label

```bash
kubectl get deployments -l env=test,app=my-client
```

#### Remove label

```
kubectl label deployments/my-dep my-label-
```

### Annotations

You can use annotations to attach arbitrary non-identifying metadata to objects.
Clients such as tools and libraries can retrieve this metadata.

### ConfigMaps

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

When a ConfigMap currently consumed in a volume is updated, projected keys are eventually updated as well enabling hot reloading if the app supports it.

### Secrets

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.
Individual secrets are limited to 1MiB in size. 
