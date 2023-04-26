# My-Kubernetes-Notes
Listing my [Kubernetes](https://kubernetes.io/docs) Notes. It will cover notes that I took from this Udemy Course(https://www.udemy.com/course/kubernetes-temelleri/).

# Introduction

1) You can access the configuration files via [here](https://github.com/aytitech/k8sfundamentals).

2) Some K8s Distributions

![here](./images/001.png)

3) Install kubernetes extension of Microsoft and Yaml extension of Redhat on Visual Studio Code.

4) K8s is highly complex.

# Kubernetes Architecture

1) Some Container Orchestration Tools are Docker Swarm, Kubernetes, Apache Mezos & Hashicorp Nomad. K8s became industry-standard. K8s has Apache 2.0 LICENSE. K8s has declerative configuration.

2) Cgroups development made by Google Engineers made containers possible.

3) Omega and Borg are 2 container orchestration tools developed by Google. They aren't open source and exist before k8s.

4) Google gave K8s to [CNCF](https://cncf.io).

5) The reasons why k8s became so popular are its design & its approach to solve the problem of container orchestration. K8s is modular. It has different components. We shouldn't tell k8s how to do. We should tell k8s what to do. Memorize carpenter analogy.

![here](./images/002.png)

6) K8s has a platform that has many multiple services(components).

7) K8s architecture is below. The left half is Master Node and the right half is Worker Nodes.

![here](./images/003.png)

8) Some k8s components:
    - kube-apiserver
    - etcd
    - kube-scheduler 
    - kube-control-manager
    - cloud controller manager

8) kube-apiserver is the most important k8s server. It can be thought as brain of K8s. It is communicating with external services and all components of k8s. All connections happen through kube-apiserver. It is a common entry-point of external services and all components of k8s.

![here](./images/004.png)

9) etcd is the second most important k8s component after kube-apiserver. It stores all cluster data, metadata information & k8s objects' information. Etcd generally is located in where kube-apiserver runs.

10) kube-scheduler is another component of k8s, which is responsible for assiging pods(~containers) to nodes(VM's).

11) kube-control-manager is tracking the system and triyng to keep desired state. Let's assume we want  our app to run on 3 pods. One pod dropped unknowingly. kube-control-monager checks data on etcd and tries to keep the number of pods as 3 by trigerring the creation of one new pod.

12) There is a component named cloud controller manager. This components exists among managed cloud k8s services on AWS, Azure and GCP.

13) kube-apiserver, etcd, kube-scheduler and kube-control-manager are known as control plane and working on master node.

14) Workload doesn't run on master nodes. Master nodes can be one or many.

15) Worker nodes have container runtime such as docker, containerd, cri-o. Each worker node has 3 main components:
    - Container runtime: Docker as default. Kubernetes stopped supporting docker runtime due to some reasons. Thus, k8s moved to containerd.
    - Kubelet: Checks etcd through API Server. Responsible for creating pods if kube-scheduler orders.
    - kube-proxy: Manages TCP, UDP SETP rules and network traffic of pods. It works as network proxy.

![here](./images/005.png)

16) K8s follows semantic versioning(x.y.z-major.minor.patch). Minor upgrades come once in 4 months. The support lasts for 12 months.

17) Some resources:
    - [https://kubernetes.io/docs](https://kubernetes.io/docs)
    - [https://github.com/kubernetes/kubernetes](https://github.com/kubernetes/kubernetes)



