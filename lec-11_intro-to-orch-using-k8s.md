Kubernetes:
- open-source container orchestration platform
- manages deployment, scaling and operations of containers
- designed for distributed systems
- focuses on resilience, scalability and automation

---

### Core Concept: Pod

Pod:
- smallest deployable unit in Kubernetes
- one or more containers running together
- containers in a pod:
  - share network (same IP)
  - share storage (volumes)
- pod is scheduled on a worker node

Execution flow:
- user creates pod
- control plane decides *where* to run it
- data plane actually runs it

---

### Kubernetes Architecture

Kubernetes has two planes:
- control plane (brain)
- data plane (execution)

---

### Control Plane Components

API Server:
- entry point to the cluster
- all commands go through API server
- exposes REST APIs (kubectl, UI, controllers)

etcd:
- distributed key-value store
- stores complete cluster state
- source of truth for Kubernetes

Controller:
- watches desired vs actual state
- takes action if mismatch occurs
- example: if replica count drops, controller creates new pods

Scheduler:
- decides which node a pod should run on
- considers:
  - CPU, memory
  - constraints, affinity
  - available resources

---

### Data Plane Components (Worker Nodes)

Kubelet:
- agent running on every node
- ensures containers in a pod are running
- talks to API server

CRI (Container Runtime Interface):
- responsible for container lifecycle
- examples: Docker, containerd, CRI-O

Kube-proxy:
- handles networking rules
- enables service networking
- manages load balancing at node level

---

### Key Features of Kubernetes

Automatic bin packing:
- schedules pods efficiently
- maximizes resource usage

Self-healing:
- restarts failed containers
- reschedules pods if node dies
- replaces unhealthy pods automatically

Horizontal scaling:
- scale number of pods up/down
- manual or automatic

Service discovery & load balancing:
- each pod gets its own IP
- services provide single DNS name
- traffic load-balanced across pods

Automated rollouts & rollbacks:
- zero-downtime deployments
- rollback to previous version if failure occurs

Secrets & config management:
- store credentials securely
- avoid baking secrets into images

Batch jobs & cron jobs:
- supports one-time jobs
- scheduled jobs (cron)

---

### Scaling in Kubernetes

Horizontal Pod Autoscaler (HPA):
- scales pod replicas
- based on CPU / memory / metrics

Vertical Pod Autoscaler (VPA):
- adjusts CPU and RAM of pods
- improves resource efficiency

Cluster Autoscaler:
- scales worker nodes
- adds nodes when pods are pending
- removes unused nodes

---

### Practical Notes

Certificates:
- Kubernetes manages certificates
- used for authentication between components

Pod lifecycle:
- deleting pod terminates containers
- resources are cleaned up automatically

---

### Key Takeaways

- pod is the smallest unit, not container
- control plane decides, data plane executes
- Kubernetes constantly maintains desired state
- built for large-scale, fault-tolerant systems
- automation is the core idea
