Kubernetes cluster setup:
- instructor used 3 machines
- 1 master node
- 2 worker nodes
- master handles control plane
- workers run application workloads

Master node setup:
- prerequisites already installed
- switched to root using `sudo su`
- initialized cluster using `kubeadm init`
- kubeadm downloads required YAMLs
- sets up:
  - API server
  - etcd
  - controller manager
  - scheduler

---

### Pods in Kubernetes

Pod:
- smallest deployable unit in Kubernetes
- can have one or more containers

Pod characteristics:
- co-located → containers run on same node
- co-scheduled → scheduled together
- share:
  - same IP
  - same network namespace
  - same storage volumes

---

### Kubernetes Architecture Recap

Two planes:

Control Plane:
- API server
- etcd (key-value store)
- controller
- scheduler
- decides *what should run and where*

Data Plane:
- worker nodes
- actually runs pods and containers

---

### kubectl & API Server

kubectl:
- command-line tool to interact with cluster
- does not talk directly to nodes

Flow:
- kubectl → API server
- API server:
  - authenticates request
  - authorizes request
  - validates request
- data stored in etcd

Communication:
- REST based (HTTP)
- kubectl is just a client

---

### Hands-on Pod Management

Instructor demo:
- creating pods using kubectl
- checking pod status

Important commands:
- `kubectl get pods`
- used to verify pod creation and state

---

### Namespaces

Namespaces:
- logical isolation inside cluster
- used to organize resources

Default namespaces:
- `default`
- `kube-system`
- others exist for internal components

---

### Networking in Kubernetes

CoreDNS:
- provides DNS inside cluster
- resolves service and pod names

Network plugins:
- required for pod-to-pod communication
- example discussed: Weave

Scheduling basics:
- scheduler places pods based on:
  - available CPU
  - available RAM
  - node capacity

---

### Key Takeaways

- master node runs control plane components
- worker nodes run pods
- pod is the smallest execution unit
- kubectl always talks to API server
- namespaces help organize cluster
- networking plugins are mandatory
- Kubernetes complexity comes from scale, not basics
