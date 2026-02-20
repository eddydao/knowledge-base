# Introduction
Kubernetes is a *portable*, *extensible*, *open source* platform for managing containerized workloads and services, both in declarative configuration and automation

## (Worker) Nodes
Software (Workloads in Kubernetes term) has to run somewhere (virtual or physical) -> Nodes

Kubernetes deploys and runs container ( Docker is the most commonly used).
In Kubernetes’s term, we deploy (scheduling in Kubernetes term) **pods**, with a pod consisting of one or more containers.
> Pods running in Nodes

## Control plane
The component that controls nodes
Do the job of: 
	- Schedule application
	- Check if all pods are in the desired state ( are all responsive or one of them need to be restarted)
	- easy to scale up by add more pods

## Scheduler 
When Scheduler discovers new pods ( containers) to be scheduled, it tries to find the optimal node for the pod -> read [[Node selection]] in Kubernetes

## Cluster
Take multiple nodes and control pane together => cluster

