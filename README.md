# My-Kubernetes-Notes
Listing my [Kubernetes](https://kubernetes.io/docs) Notes. It will cover notes that I took from this Udemy Course(https://www.udemy.com/course/kubernetes-temelleri/).

# Introduction

1) You can access the configuration files via [here](https://github.com/aytitech/k8sfundamentals).

2) Some K8s Distributions

![here](./images/001.png)

3) Install kubernetes extension of Microsoft and Yaml extension of Redhat on Visual Studio Code.

4) K8s is highly complex.

5) K8s is a container orchestration tool. It isn't a container engine tool. Docker, containerd and cri-o are [container engines](https://phoenixnap.com/kb/docker-vs-containerd-vs-cri-o) that k8s supports.

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

8) kube-apiserver is the most important k8s server. It can be thought as brain of K8s. It is communicating with external services and all components of k8s. All connections happen through kube-apiserver. It is a common entry-point of external services and all components of k8s. kube-apiserver is a REST API Server.

![here](./images/004.png)

9) etcd is the second most important k8s component after kube-apiserver. It stores all cluster data, metadata information & k8s objects' information. Etcd generally is located in where kube-apiserver runs.

10) kube-scheduler is another component of k8s, which is responsible for assiging pods(~containers) to nodes(VM's).

11) kube-control-manager is tracking the system and triyng to keep desired state. Let's assume we want  our app to run on 3 pods. One pod dropped unknowingly. kube-control-monager checks data on etcd and tries to keep the number of pods as 3 by trigerring the creation of one new pod.

12) There is a component named cloud controller manager. This components exists among managed cloud k8s services on AWS, Azure and GCP.

13) kube-apiserver, etcd, kube-scheduler and kube-control-manager are known as control plane and working on master node.

14) Workload doesn't run on master nodes. Master nodes can be one or many.

15) Worker nodes have container runtime such as docker, containerd, cri-o. Each worker node has 3 main components:
    - Container runtime: Docker as default. Kubernetes stopped supporting docker runtime due to some reasons. Thus, k8s moved to containerd as of k8s 1.20.1 .
    - Kubelet: Checks etcd through API Server. Responsible for creating pods if kube-scheduler orders.
    - kube-proxy: Manages TCP, UDP SETP rules and network traffic of pods. It works as network proxy.

![here](./images/005.png)

16) K8s follows semantic versioning(x.y.z-major.minor.patch). Minor upgrades come once in 4 months. The support lasts for 12 months.

17) Some resources:
    - [https://kubernetes.io/docs](https://kubernetes.io/docs)
    - [https://github.com/kubernetes/kubernetes](https://github.com/kubernetes/kubernetes)

# Kubernetes Installation

1) There are 3 ways to communicate with API Server

    - REST Calls(via curl or via program)
    - GUI(official dashboard is Kubernetes Dashboard, Lens, Octant etc.)
    - CLI( kubectl )

2) Install kubectl via [instruction listed here](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

3) Chocolatey is a package manager for Windows. It does what MacOS's Homebrew does.

4) We can install kubectl via snap or brew. To check the version of kubectl, run the following:

```version.sh
kubectl version --client
```

5) minikube and Docker Desktop should be used for development and testing purposes.

6) kubeadm is semi-official version K8s for production purposes. There are more k8s packages for production like k0s, kubespray, RKE. There are spported and paid k8s solutions from enterprise companies.

7) Public cloud managed K8s solutions exist among AWS(EKS - Elastic Kubernetes Service), Azure(AKS - Azure Kubernetes Service) and GCP(GKE - Google Kubernetes Engine).

8) We can install a single-node k8s via Docker Desktop. In order to install Docker Desktop, we should enable virtualization first for our OS. We can enable k8s on Docker Desktop. After enabling k8s on Docker Desktop, we can see that Server Version is also enabled.

9) [Minikube](https://minikube.sigs.k8s.io/docs/start/) is preferred over Docker Desktop. Docker Desktop is not available on Linux. Minikube is installing a single-node k8s cluster locally. We can change it to multi-nodes later in Minikube.

10) In order to install Minikube, docker or podman or VMWare or Hyper-V should exist in our computer.

11) We can start a k8s cluster via the command below

```start.sh
# To start with default driver(probably docker)
minikube start
# To start with a different driver
minikube start --driver=vmware
minikube start --driver=podman

```

12) To check status of k8s cluster triggered via minikube,

```status.sh
minikube status
```

    - minikube
    - type: Control Plane
    - host: Running
    - kubelet: Running
    - apiserver: Running
    - kubeconfig: Configured

13) To list nodes of k8s cluster

```list.sh
kubectl get nodes
```

14) To purge k8s cluster

```delete.sh
minikube delete
```

15) To stop a existing k8s cluster without deleting

```stop.sh
minikube stop
```

16) Azure is providing 200$ free credit for one month. We don't pay for master node in AKS. We just pay for worker nodes. In order to use AKS from local computers, we should install Azure CLI in our local computers. After installing CLI, run `az login` on Terminal and enter the credentials. To list resource groups, run `az group list` or `az group list -o table`. To bind our kubectl to AKS, trigger `az aks get-credentials --name NAME_OF_K8S_ON_AZ --resource-group RESOURCE_GROUP_OF_AKS_CLUSTER`. After completing our job, we should delete AKS cluster on Azure.

17) GCP is proving GKE(Google Kubernetes Engine). Download and install GCP's CLI. Then connect our CLI to GCP. Then, connect to GKE on GCP. No master node fees exist. Only paying for worker nodes.

18) AWS EKS is charging money for master nodes unlike Azure and GCP. Install AWS CLI and connect kubectl to remote EKS cluster. Creating nodes in AWS for EKS takes so much time.

## kubeadm

19) kubeadm is a way to create k8s clusters efficiently using following best practices. We can use kubeadm to create a cluster composed of many machines(Bare metal, VM's, Cloud VM's, Rasperry pi etc)

20) [multipass.run](https://multipass.run) by Canonical is a way to run ubuntu VM's using CLI easily. It is required to have Hyper-v or VirtualBox among our system. Multipass faciliates creating processes of VM's.

21) Windows 10 Pro/Enterprise and Education have Hyper-V by default.

22) Follow the instructions [here](https://github.com/aytitech/k8sfundamentals/tree/main/setup) and set up a k8s cluster on local machine using kubeadm. 

23) `multpass shell MACHINE_NAME` is a way to connect to the multipass instance.

24) Some components of k8s are working on containers too. Api-server, controller-manager, kube-scheduler, kube-proxy are pulled from container registry platform and running on docker containers to make up of k8s.

25) The machine where `sudo kubeadm init` is triggered is the master node of k8s cluster.

26) When we set up a cluster, it is required to install a plug-in to manage the network. The most famous one is [Calico](https://docs.tigera.io/calico/latest/getting-started/kubernetes/).

27) We can use [play-with-k8s](https://labs.play-with-k8s.com/) to use k8s if we can't install k8s on local computer os we can't use cloud services.





